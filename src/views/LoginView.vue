<script lang="ts" setup>
import axios from "axios";
import { ref } from 'vue';
import { useRouter } from "vue-router";

const router = useRouter();

const user_email = ref('');
const user_password = ref('');

const loginUser = () => {
  // 在这里可以执行登录逻辑，发送用户输入到后端进行验证
  // 你可以使用 Axios 或 Fetch API 来发送登录请求

  // 构建一个包含用户登录信息的对象
  const userData = {
    user_email: user_email.value,
    user_password: user_password.value,
  };

  // 发送用户数据到后端登录接口
  axios.post('/api/login', userData)
    .then(response => {
      if (response.data.error) {
        // 处理登录错误
        alert('登入失敗：' + response.data.error);
      } else {
        // 处理成功登录的情况
        alert('登入成功');

        // 你可以执行页面跳转或其他操作
        // 例如，使用 Vue Router 来跳转到用户的个人资料页
        router.push({ name: 'message' }); // 假设你有一个名为 'profile' 的路由
      }
    })
    .catch(error => {
      console.error('網路異常：', error);
    });
};
</script>

<template>
  <div class="login flex items-center justify-center bg-gray-100 m-48">
    <div class="max-w-md w-full p-4 bg-white rounded-lg shadow-md border-2">
      <h2 class="text-2xl font-semibold text-center mb-4">使用者登入</h2>
      <form @submit.prevent="loginUser">
        <div class="mb-4">
          <label for="user_email" class="block text-sm font-medium text-gray-600">電子郵件</label>
          <input type="text" id="user_email" v-model="user_email" required
                 class="w-full px-4 py-2 rounded-md border focus:ring-indigo-500 focus:border-indigo-500
                 shadow-sm focus:ring-2 focus:ring-offset-2">
        </div>
        <div class="mb-4">
          <label for="user_password" class="block text-sm font-medium text-gray-600">密碼</label>
          <input type="password" id="user_password" v-model="user_password" required
                 class="w-full px-4 py-2 rounded-md border focus:ring-indigo-500 focus:border-indigo-500
                 shadow-sm focus:ring-2 focus:ring-offset-2">
        </div>
        <button type="submit" class="w-full px-4 py-2 rounded-md bg-indigo-600 text-white hover:bg-indigo-700
            focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">登入</button>
      </form>
    </div>
  </div>
</template>


