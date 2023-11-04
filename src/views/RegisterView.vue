<template>
  <div class="register flex items-center justify-center bg-gray-100 m-48">
    <div class="max-w-md w-full p-4 bg-white rounded-lg shadow-md border-2">
    <h2 class="text-2xl font-semibold mb-4">使用者註冊</h2>
    <form @submit.prevent="registerUser">
      <div class="mb-4">
        <label class="block font-medium" for="username">使用者名稱</label>
        <input v-model="formData.username" id="username" type="text" required class="border rounded-md py-2 px-3 w-full">
      </div>
      <div class="mb-4">
        <label class="block font-medium" for="email">電子郵件</label>
        <input v-model="formData.email" id="email" type="email" required class="border rounded-md py-2 px-3 w-full">
      </div>
      <div class="mb-4">
        <label class="block font-medium" for="password">密碼</label>
        <input v-model="formData.password" id="password" type="password" required
          class="border rounded-md py-2 px-3 w-full">
      </div>
      <button type="submit" class="w-full px-4 py-2 rounded-md bg-indigo-600 text-white hover:bg-indigo-700
            focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">註冊</button>
    </form>
  </div>
</div>
</template>

<script setup>
import axios from "axios";
import { ref } from 'vue';
import { useRouter } from "vue-router";

const router = useRouter();

const formData = ref({
  username: '',
  email: '',
  password: ''
});

const registerUser = () => {
  // 在这里可以进行前端验证，确保提供了必要的注册信息

  // 构建一个包含用户信息的对象
  const userData = {
    user_name: formData.value.username,
    user_password: formData.value.password,
    user_email: formData.value.email
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
        alert('註冊成功，即將回到登入畫面');
        // 可以重定向到登录页面或执行其他操作
        setTimeout(() => {
          // 假设注册成功后重定向到登录页面
          router.push({ name: 'login' });
        }, 1000); // 在1秒后跳转
      }
    })
    .catch(error => {
      console.error('無法註冊：', error);
    });
};
</script>
