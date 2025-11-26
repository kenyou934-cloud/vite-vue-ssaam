<template>
  <div class="loading-screen">
    <div class="flex flex-col items-center justify-center gap-6 text-center">
      <div class="w-32 h-32 flex items-center justify-center animate-bounce">
        <img :src="jrmsuLogo" alt="JRMSU CCS Logo" class="w-full h-full object-contain drop-shadow-2xl" />
      </div>
      <div>
        <h1 class="text-4xl font-bold text-white mb-2">SSAAM LOGO</h1>
        <p class="text-lg text-white opacity-90">Student School Activities Attendance Monitoring</p>
      </div>
      <div class="flex gap-2 mt-8">
        <div class="w-3 h-3 rounded-full bg-white animate-pulse"></div>
        <div class="w-3 h-3 rounded-full bg-white animate-pulse" style="animation-delay: 0.2s;"></div>
        <div class="w-3 h-3 rounded-full bg-white animate-pulse" style="animation-delay: 0.4s;"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'
import jrmsuLogo from '../assets/jrmsu-logo.webp'

const router = useRouter()

onMounted(() => {
  setTimeout(() => {
    router.push('/')
  }, 2000)
})
</script>