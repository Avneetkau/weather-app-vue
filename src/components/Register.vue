<script setup>
import { ref, reactive } from 'vue'

const warningText = reactive({
  email: '',
  password: '',
  confirmpassword: ''
})
const emit = defineEmits(['updateRgisterStatus'])

const props = defineProps({
  registerData: {
    type: Object,
    required: true
  }
})
const validate = () => {
  if ('' == props.registerData.email) {
    warningText.email = 'Email required'
    return false
  }
  if ('' == props.registerData.password) {
    warningText.password = 'Password Required'
    return false
  }
  if (
    '' == props.registerData.confirmpassword ||
    props.registerData.password !== props.registerData.confirmpassword
  ) {
    warningText.confirmpassword = "Confirm password doesn't match with the password"
    return false
  }
  return true
}
const registration = () => {
  let validation = validate()
  if (validation) {
    console.log('success')
    warningText.email = ''
    warningText.password = ''
    warningText.confirmpassword = ''
    localStorage.setItem('user', JSON.stringify(props.registerData))
    emit('updateRgisterStatus', true)
  }
}
</script>

<template>
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username"> Email </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        id="email"
        type="email"
        v-model="registerData.email"
        placeholder="email"
      />
      <p class="text-red-500 text-xs italic">{{ warningText.email }}</p>
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="password"> Password </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
        id="password"
        type="password"
        v-model="registerData.password"
        placeholder="******************"
      />
      <p class="text-red-500 text-xs italic">{{ warningText.password }}</p>
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
        Confirm Password
      </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
        id="password"
        type="password"
        v-model="registerData.confirmpassword"
        placeholder="******************"
      />
      <p class="text-red-500 text-xs italic">{{ warningText.confirmpassword }}</p>
    </div>
    <div class="flex items-center justify-between">
      <button
        @click.prevent="registration()"
        class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="button"
      >
        Rerister
      </button>
    </div>
  </form>
</template>

<style scoped></style>
