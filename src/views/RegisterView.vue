<script setup>
import Register from '@/components/Register.vue';
import Login from '@/components/Login.vue';
import { ref, reactive } from 'vue';
import router from '@/router';

const registerSuccess = ref(false);
const loginSuccess = ref(false);
const loginRegisterTxt = ref('');
const titleText = ref('Register');
const registerData = reactive({
  email: '',
  password: '',
  confirmpassword: '',
});
const updateRgisterStatus = (status) => {
  registerSuccess.value = status;
  loginRegisterTxt.value = 'You have Successfully Registered';
  titleText.value = 'Login';
};
const updateLoginStatus = (status) => {
  loginSuccess.value = status;
  if (status) {
    router.push({ path: '/' });
  }
};
</script>

<template>
  <section class="flex h-screen w-full">
    <template v-if="!loginSuccess">
      <div class="w-full flex flex-col justify-center items-center bg-gray-200">
        <h2 class="mb-5 text-xl">{{ titleText }}</h2>
        <p v-show="registerSuccess && loginRegisterTxt" class="text-green-500 text-xs italic mb-3">
          {{ loginRegisterTxt }}
        </p>
        <div class="w-full max-w-xs">
          <Register
            v-if="!registerSuccess"
            @updateRgisterStatus="updateRgisterStatus"
            :registerData="registerData"
          ></Register>
          <Login @updateLoginStatus="updateLoginStatus" v-else></Login>

          <p
            v-if="titleText == 'Register'"
            class="text-black-500 text-xs italic mb-3 mt-3 text-center"
          >
            Already have a account
            <span
              class="cursor-pointer text-blue-500 font-bold"
              @click.prevent="
                registerSuccess = true;
                titleText = 'Login';
              "
              >Sign In</span
            >
          </p>

          <p
            v-if="titleText == 'Login'"
            class="text-black-500 text-xs italic mb-3 mt-3 text-center"
          >
            Don't have a account
            <span
              class="cursor-pointer text-blue-500 font-bold"
              @click.prevent="
                registerSuccess = false;
                titleText = 'Register';
              "
              >Register</span
            >
          </p>
        </div>
      </div>
    </template>
    <!-- <template v-else>
      <div class="w-full">
        <h1 class="mb-5 text-2xl mt-10 text-white text-center">Home Page</h1>
        <h3 class="text-green-500 text-xs italic mb-3 text-center">
          Now you are Successfully Loged In
        </h3>
      </div>
    </template> -->
  </section>
</template>
<style scoped></style>
