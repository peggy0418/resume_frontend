<template>
  <div class="register">
    <h2>使用者註冊</h2>
    <form @submit.prevent="registerUser">
      <div class="form-group">
        <label for="user_name">使用者名稱</label>
        <input type="text" id="username" v-model="formData.username" required>
      </div>
      <div class="form-group">
        <label for="user_email">電子郵件</label>
        <input type="email" id="email" v-model="formData.email" required>
      </div>
      <div class="form-group">
        <label for="user_password">密碼</label>
        <input type="password" id="password" v-model="formData.password" required>
      </div>
      <button type="submit">送出</button>
    </form>
  </div>
</template>
  
<script>
import axios from "axios";
export default {
  data() {
    return {
      formData: {
        user_name: '',
        user_email: '',
        user_password: ''
      }
    };
  },
  methods: {
    registerUser() {
      // 在这里可以进行前端验证，确保提供了必要的注册信息

      // 构建一个包含用户信息的对象
      const userData = {
        user_name: this.formData.username,
        user_password: this.formData.password,
        user_email: this.formData.email
      };

      // 发送用户数据到后端注册接口，可以使用Axios或其他方法
      // 例如，使用Axios发送POST请求
      axios.post('/api/register', userData)
        .then(response => {
          if (response.data.error) {
            // 处理注册错误
            alert('無法註冊');
          } else {
            // 处理成功注册的情况
            alert('註冊成功');
            // 可以重定向到登录页面或执行其他操作
            setTimeout(() => {
              // 假设注册成功后重定向到登录页面
              this.$router.push({ name: 'login' });
            }, 1000); // 在1秒后跳转
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
.register {
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
input[type="email"],
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