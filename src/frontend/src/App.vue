<script setup>
import {reactive, ref} from 'vue';
import { useReCaptcha } from 'vue-recaptcha-v3'

const user = reactive({ username: '', password: '' });
const { executeRecaptcha, recaptchaLoaded } = useReCaptcha()

const onSubmit = async () => {
  // (optional) Wait until recaptcha has been loaded.
  await recaptchaLoaded()

  // Execute reCAPTCHA with action "login".
  const token = await executeRecaptcha('login')
  console.log("token:",token);
  console.log("user:",user);

  // Send the token as a header to the login endpoint
  fetch('http://localhost:8080/api/auth/token', {
    method: 'POST',
    headers: {
      'recaptcha': token,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(user)
  })
  .then(r => r.text())
  .then(data => {
    console.log("jwt:",data)
  });

}
</script>


<template>
  <div class="min-h-screen flex bg-gray-200">
    <form class="w-1/4 m-auto bg-white p-8 border border-gray-400 rounded-md shadow-md" @submit.prevent="onSubmit">
      <div class="mt-6">
        <label for="username" class="block text-gray-700 text-sm font-bold mb-2">Username</label>
        <input type="text" id="username" v-model="user.username"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          placeholder="Username">
      </div>
      <div class="mt-6">
        <label for="password" class="block text-gray-700 text-sm font-bold mb-2">Password</label>
        <input type="password" id="password" v-model="user.password"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          placeholder="******************">
      </div>
      <div class="flex justify-end">
        <button
          class="g-recaptcha bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
          Sign In
        </button>
      </div>
    </form>
  </div>
</template>

