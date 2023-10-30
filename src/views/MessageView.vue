<template>
  <div id="app" class="message">
    <h1>留言板</h1>
    姓名: <input v-model="newSender" placeholder="輸入姓名"><br />
    內容: <input v-model="newMessage" placeholder="輸入留言"><br />
    <button @click="addSenderAndMessage">送出</button>
    <ul>
      <h1>留言列表</h1>
      <li v-for="message in messages" :key="message.msg_id">
        <p>姓名: {{ message.sender }}</p>
        <p v-if="message.msg_id !== editingMessage">{{ message.message }}</p>
        <input v-else v-model="editedMessage">
        <button @click="message.msg_id === editingMessage ? updateMessage(message.msg_id) : editMessage(message)">
          {{ message.msg_id === editingMessage ? '儲存' : '編輯' }}
        </button> | 
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
      editingMessage: null,
      editedMessage: '',
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
    editMessage(message) {
      this.editedMessage = message.message;
      this.editingMessage = message.msg_id;
    },
    updateMessage(msg_id) {
      axios.put(`/api/messages/${msg_id}`, { message: this.editedMessage })
        .then(response => {
          this.messages = this.messages.map(message => {
            if (message.msg_id === msg_id) {
              message.message = this.editedMessage;
            }
            return message;
          });
          this.editingMessage = null;
          this.editedMessage = '';
          alert('儲存成功！');
        })
        .catch(error => {
          console.error('更新錯誤：', error);
        });
    },
    deleteMessage(msg_id) {
      axios.delete(`/api/messages/${msg_id}`)
        .then(response => {
          this.messages = this.messages.filter(message => message.msg_id !== msg_id);
          alert('刪除成功!');
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
