<template>
    <div class="login">
      <h2>使用者登入</h2>
      <form @submit.prevent="loginUser">
        <div class="form-group">
          <label for="user_email">電子郵件</label>
          <input type="text" id="user_email" v-model="user_email" required>
        </div>
        <div class="form-group">
          <label for="user_password">密碼</label>
          <input type="password" id="user_password" v-model="user_password" required>
        </div>
        <button type="submit">登入</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from "axios"
  export default {
    data() {
      return {
        user_email: '',
        user_password: ''
      };
    },
    methods: {
      loginUser() {
        // 在这里可以执行登录逻辑，发送用户输入到后端进行验证
        // 你可以使用 Axios 或 Fetch API 来发送登录请求
  
        // 构建一个包含用户登录信息的对象
        const userData = {
          user_email: this.user_email,
          user_password: this.user_password
        };
  
        // 发送用户数据到后端登录接口
        axios.post('/api/login', userData)
          .then(response => {
            if (response.data.error) {
              // 处理登录错误
              alert('登录失败：' + response.data.error);
            } else {
              // 处理成功登录的情况
              alert('登录成功：' + response.data.message);
  
              // 你可以执行页面跳转或其他操作
              // 例如，使用Vue Router来跳转到用户的个人资料页
              this.$router.push({ name: 'message' }); // 假设你有一个名为'profile'的路由
            }
          })
          .catch(error => {
            console.error('发生网络错误：', error);
          });
      }
    }
  };
  </script>
  
  
  <style scoped>
  .login {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    font-weight: bold;
  }
  
  input[type="text"],
  input[type="password"] {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
  }
  
  button {
    background-color: #007bff;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>
  