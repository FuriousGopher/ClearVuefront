<template>
  <div class="login-wrapper">
    <div class="login-header">
      <img src="/backOffice.png" alt="logo" />
    </div>
    <div class="login-board">
      <div class="login-container">
        <h4>Login</h4>
        <form @submit.prevent="userLogin">
          <div class="form-group">
            <label for="username">Email: testIvan@gmail.com</label>
            <input type="text" id="username" v-model="email" required />
          </div>
          <div class="form-group">
            <label for="password">Password: q1w2e3r4</label>
            <input type="password" id="password" v-model="password" required />
          </div>
          <button type="submit">Login</button>
        </form>
        <p>If you dont have access ask your manager</p>
        <div class="client-button">
          <button @click="clientLogin">I'm a client</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toast-notification'
import 'vue-toast-notification/dist/theme-sugar.css'
import router from '@/router/index.ts'
import { login } from '@/api/agentApi.ts'

const email = ref('')
const password = ref('')
const $toast = useToast()

const userLogin = async () => {
  try {
    await login({ email: email.value, password: password.value })
    $toast.success('Successfully logged in')
    router.push('/home')
  } catch (e) {
    $toast.error(e.response.data)
  }
}

const clientLogin = async () => {
  try {
    router.push('/client')
  } catch (e) {
    $toast.error(e.response.data)
  }
}
</script>

<style scoped>
.login-board {
  display: flex;
  height: calc(80vh - 200px);
}

.login-container {
  justify-content: center;
  align-items: center;
  padding: 40px 80px;
  margin: auto;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}
.form-group {
  margin-bottom: 15px;
}

h4 {
  text-align: center;
}

label {
  display: block;
  margin-bottom: 5px;
}

.login-wrapper {
  display: flex;
  flex-direction: column;
}

h2 {
  text-align: center;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

button {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 3px;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
  margin-bottom: 10px;
}

.login-header {
  text-align: center;
  margin-bottom: -60px;
}

button:hover {
  background-color: #0056b3;
}
</style>
