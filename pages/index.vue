<template>
  <div class="min-h-screen flex items-center justify-center bg-gradient-to-bl from-gray-400 via-gray-600 to-blue-800">
    <div class="max-w-lg w-full bg-gray-300 p-8 rounded-lg shadow-lg">
      <div class="flex items-center justify-center">
        <div lg:w-[500px] relative>
          <img
            src="@/assets/logo.png"
            alt="Fnote logo"
            class="relative w-full h-40"
          />
        </div>
      </div>
      <h1 class="text-3xl font-bold text-center mb-1">Selamat datang di Fnote</h1>
      <p class="text-base text-center">
        <span class="text-lg italic font-bold">Fnote adalah</span> aplikasi catatan yang dirancang untuk 
        membantu seseorang untuk mencatat ide, daftar tugas, 
        dan informasi penting dengan mudah dan efisien.
      </p>
      <h2 class="text-2xl font-bold text-center mb-1">Login</h2>
      <form @submit.prevent="login">
        <div class="mb-4">
          <label for="email" class="block text-gray-700 mb-1">Email</label>
          <input
            type="email"
            id="email"
            v-model="email"
            class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring focus:border-blue-300"
          />
        </div>
        <div class="mb-1">
          <label for="password" class="block text-gray-700">Password</label>
          <input
            type="password"
            id="password"
            v-model="password"
            class="w-full mb-1 px-4 py-2 border rounded-lg focus:outline-none focus:ring focus:border-blue-300"
          />
        </div>
        <p v-if="errorMessage" class="text-red-500 text-center mb-2">{{ errorMessage }}</p>
        <p class="text-center mb-1 mt-1">Belum punya akun? <a href="/signup" class="text-blue-500 hover:underline">Signup</a></p>
        <button
          type="submit"
          class="w-full py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-700 transition duration-300 mt-3"
        >Login
        </button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { signInWithEmailAndPassword } from 'firebase/auth'
import { auth } from '~/plugins/firebase'

const email = ref<string>('')
const password = ref<string>('')
const errorMessage = ref<string>('')

const router = useRouter()

const login = async () => {
  try {
    const userCredential = await signInWithEmailAndPassword(auth, email.value, password.value)
    console.log('Login successful:', userCredential)
    // Redirect to dashboard after successful login
    router.push('/dashboard')
  } catch (error) {
    console.error('Login error:', error)
    errorMessage.value = 'Invalid email or password.'
  }
}
</script>

<style scoped>
</style>
