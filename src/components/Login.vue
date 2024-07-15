<script setup>
import { ref, reactive } from 'vue';

const loginData = reactive({
  email: '',
  password: '',
});
const warningText = reactive({
  email: '',
  password: '',
});

const emit = defineEmits(['updateLoginStatus']);
const checkLogin = () => {
  let userInfo = JSON.parse(localStorage.getItem('user'));

  if (userInfo.email !== loginData.email) {
    warningText.email = "Email doesn't match";
    return false;
  }
  if (userInfo.password !== loginData.password) {
    warningText.password = "Password doesn't match";
    return false;
  }
  return true;
};
const logIn = () => {
  let isLogin = checkLogin();
  if (isLogin) {
    warningText.email = '';
    warningText.password = '';
    emit('updateLoginStatus', true);
  }
};
</script>

<template>
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username"> Email </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        id="username"
        type="email"
        v-model="loginData.email"
        placeholder="Email"
      />
      <p class="text-red-500 text-xs italic">{{ warningText.email }}</p>
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="password"> Password </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
        id="password"
        type="password"
        v-model="loginData.password"
        placeholder="******************"
      />
      <p class="text-red-500 text-xs italic">{{ warningText.password }}</p>
    </div>
    <div class="flex items-center justify-between">
      <button
        @click.prevent="logIn()"
        class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="button"
      >
        Sign In
      </button>
    </div>
  </form>
</template>

<style scoped></style>
