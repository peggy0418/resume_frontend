<template>
  <div id="app" class="message">
    <h1>留言板</h1>
    姓名: <input v-model="newSender" placeholder="輸入姓名"><br />
    內容: <input v-model="newMessage" placeholder="輸入留言"><br />
    <button @click="addSenderAndMessage">送出</button>
    <ul>
      <h1>留言列表</h1>
      <li v-for="message in messages" :key="message.msg_id">
        <!-- <p>編號: {{ message.msg_id }}</p> -->
        <p>姓名: {{ message.sender }}</p>
        <p>內容: {{ message.message }}</p>
        <button @click="deleteMessage(message.msg_id)">刪除</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      newSender: '',
      newMessage: '',
      senders: [],
      messages: [],
    };
  },
  created() {
    this.loadMessages();
  },
  methods: {
    addSenderAndMessage() {
      axios.post('/api/messages', { sender: this.newSender, message: this.newMessage })
        .then(response => {
          this.newSender = '';
          this.newMessage = '';
          this.loadMessages();
        })
        .catch(error => {
          console.error('發生錯誤：', error);
        });
    },

    loadMessages() {
      axios.get('/api/messages')
        .then(response => {
          this.messages = response.data;
        })
        .catch(error => {
          console.error('發生錯誤：', error);
        });
    },
    deleteMessage(msg_id) {
      axios.delete(`/api/messages/${msg_id}`)
        .then(response => {
          // 删除成功后从messages数组中移除被删除的消息
          this.messages = this.messages.filter(message => message.msg_id !== msg_id);
          alert('刪除成功!')
        })
        .catch(error => {
          console.error('刪除錯誤：', error);
        });
    }
  },
};
</script>

<style>
.message {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
