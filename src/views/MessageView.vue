<template id="app" class="message">
  <div class="m-4">
  <h1 class="text-3xl font-semibold mb-4">留言板</h1>
  <div class="shadow-2xl p-4">
    <div class="mb-4">
      <label for="sender" class="block font-medium">姓名:</label>
      <input v-model="newSender" id="sender" class="border rounded-md py-2 px-3 w-1/2" placeholder="輸入姓名">
    </div>
    <div class="mb-4">
      <label for="message" class="block font-medium">內容:</label>
      <input v-model="newMessage" id="message" class="border rounded-md py-2 px-3 w-1/2" placeholder="輸入留言">
    </div>
    <button @click="addSenderAndMessage" type="button"
      class="rounded-md bg-black/10 px-2.5 py-1.5 text-sm font-semibold shadow-sm hover:bg-black/20">
      送出
    </button>
  </div>

  <div class="shadow-2xl p-4">
    <ul class="mt-8">
      <h2 class="text-xl font-semibold">留言列表</h2>
      <li v-for="message in messages" :key="message.msg_id" class="mt-4">
        <p class="font-medium">姓名: {{ message.sender }}</p>
        <p v-if="message.msg_id !== editingMessage" class="mt-2">內容:{{ message.message }}</p>
        <input v-else v-model="editedMessage" class="border rounded-md py-2 px-3 mt-2 w-1/2">
        
        <span class="isolate inline-flex rounded-md shadow-sm">
          <button @click="message.msg_id === editingMessage ? updateMessage(message.msg_id) : editMessage(message)"
          class="rounded-md bg-black/10 px-2.5 py-1.5 text-sm font-semibold shadow-sm hover:bg-black/20">
          {{ message.msg_id === editingMessage ? '儲存' : '編輯' }}
        </button>
        <button @click="deleteMessage(message.msg_id)"
          class="bg-red-500 hover:bg-red-600 text-white rounded-md px-2.5 py-1.5 text-sm font-semibold shadow-sm">
          刪除
        </button>
        </span>
      </li>
    </ul>
  </div>
  </div>
</template>

<!-- The rest of your script and style sections remain unchanged -->


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
}</style>
