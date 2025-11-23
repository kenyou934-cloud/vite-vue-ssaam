<template>
  <div class="min-h-screen flex bg-gradient-to-br from-purple-600 via-purple-500 to-pink-400">
    <div class="w-1/2 flex flex-col items-center justify-center text-white p-12 relative">
      <div class="absolute inset-0 bg-white bg-opacity-10"></div>
      <div class="relative z-10 text-center">
        <div class="mb-8">
          <div class="w-64 h-64 mx-auto mb-4 flex items-center justify-center">
            <img src="/src/assets/jrmsu-logo.webp" alt="JRMSU CCS Logo" class="w-full h-full object-contain drop-shadow-2xl" />
          </div>
        </div>
        <h1 class="text-5xl font-bold mb-4">SSAAM LOGO</h1>
        <p class="text-xl">Student School Activities Attendance Monitoring</p>
      </div>
      <div class="absolute bottom-4 left-4 text-sm text-white opacity-75">
        Copyright © 2025 Powered by CCS-Creatives Committee. Chairperson: Sheen Lee
      </div>
    </div>

    <div class="w-1/2 flex items-center justify-center p-12">
      <div class="bg-white rounded-3xl shadow-2xl p-10 w-full max-w-md">
        <div class="mb-8 text-center">
          <h2 class="text-3xl font-bold text-purple-900 mb-2">Let's Get Started!</h2>
          <p class="text-gray-600 text-sm mb-4">You are a few clicks away from your profile.</p>
          <p class="text-gray-600 text-sm">Input your JRMSU Student ID to continue.</p>
        </div>

        <div class="flex mb-6 border-b border-gray-200">
          <button 
            class="flex-1 py-3 px-4 text-center font-medium border-b-2 border-purple-600 text-purple-600"
          >
            Log In
          </button>
          <button 
            @click="goToRegister"
            class="flex-1 py-3 px-4 text-center font-medium text-gray-500 hover:text-gray-700"
          >
            👤 Register
          </button>
        </div>

        <form @submit.prevent="handleLogin" class="space-y-6">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Student ID</label>
            <div class="relative">
              <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
              <input
                v-model="studentId"
                type="text"
                placeholder="25-A-12345"
                class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                required
              />
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
            <div class="relative">
              <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">🔑</span>
              <input
                v-model="password"
                type="password"
                placeholder="Your Password (Last Name)"
                class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                required
              />
            </div>
          </div>

          <button
            type="submit"
            class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center"
          >
            Login
            <span class="ml-2">→</span>
          </button>

          <div class="text-center text-sm text-gray-600">
            Need help? <a href="#" class="text-purple-600 hover:underline">Contact us</a>
          </div>
        </form>

        <div class="mt-6 text-center text-xs text-gray-500">
          Powered by <span class="text-yellow-500 font-medium">CCS - Creatives Committee</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const studentId = ref('')
const password = ref('')

const handleLogin = () => {
  const users = JSON.parse(localStorage.getItem('users') || '[]')
  const user = users.find(u => u.studentId === studentId.value && u.lastName.toLowerCase() === password.value.toLowerCase())
  
  if (user) {
    localStorage.setItem('currentUser', JSON.stringify(user))
    router.push('/dashboard')
  } else if (studentId.value === 'admin' && password.value === 'admin') {
    localStorage.setItem('currentUser', JSON.stringify({ role: 'admin', name: 'ADMIN' }))
    router.push('/dashboard')
  } else {
    alert('Invalid credentials! Please try again.')
  }
}

const goToRegister = () => {
  router.push('/register')
}
</script>