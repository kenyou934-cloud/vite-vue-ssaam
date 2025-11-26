<template>
  <div id="app">
    <LoadingScreen v-if="isLoading" />
    <router-view v-if="!isLoading" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import LoadingScreen from './components/LoadingScreen.vue'

const isLoading = ref(true)

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 2000)
})
</script>

<style>
#app {
  width: 100%;
  height: 100vh;
}
</style>