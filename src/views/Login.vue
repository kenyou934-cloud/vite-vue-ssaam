<template>
  <div v-if="showErrorNotification" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-2xl shadow-2xl p-8 max-w-sm w-full mx-4 text-center transform transition-all">
      <div class="w-20 h-20 mx-auto mb-4 bg-red-100 rounded-full flex items-center justify-center">
        <svg class="w-12 h-12 text-red-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
        </svg>
      </div>
      <h3 class="text-2xl font-bold text-purple-900 mb-2">Oops!</h3>
      <p class="text-gray-600">{{ errorMessage }}</p>
      <button @click="showErrorNotification = false" class="mt-6 px-6 py-2 bg-gradient-to-r from-purple-600 to-pink-500 text-white rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300">
        Try Again
      </button>
    </div>
  </div>

  <div v-if="showDevelopersPopup" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50" @click.self="showDevelopersPopup = false">
    <div class="bg-white rounded-2xl shadow-2xl p-8 max-w-lg w-full mx-4">
      <div class="flex justify-between items-center mb-6">
        <h3 class="text-2xl font-bold text-purple-900">Meet Our Developers</h3>
        <button @click="showDevelopersPopup = false" class="text-gray-500 hover:text-gray-700 text-2xl">&times;</button>
      </div>
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-4 mb-6">
        <a v-for="dev in developers" :key="dev.name" :href="dev.facebook" target="_blank" rel="noopener noreferrer" class="flex flex-col items-center cursor-pointer hover:transform hover:scale-105 transition">
          <div class="w-16 h-16 rounded-full bg-gradient-to-br from-purple-500 to-pink-400 flex items-center justify-center text-white text-2xl shadow-lg mb-2 overflow-hidden">
            <img v-if="dev.image" :src="dev.image" :alt="dev.name" class="w-full h-full object-cover" />
            <span v-else>{{ dev.initials }}</span>
          </div>
          <p class="text-xs font-semibold text-purple-600 hover:text-purple-800 text-center">{{ dev.name }}</p>
          <p class="text-xs text-gray-500 text-center">{{ dev.role }}</p>
        </a>
      </div>
      <div class="text-center text-sm text-gray-600">
        <p class="font-medium text-purple-900">CCS - Creatives Committee</p>
        <p>Chairperson: Sheen Lee</p>
      </div>
    </div>
  </div>

  <div class="hidden md:flex min-h-screen bg-white">
    <div class="desktop-bg-panel">
      <div class="relative z-10 text-center">
        <div class="mb-4">
          <div class="w-40 h-40 mx-auto flex items-center justify-center">
            <img :src="jrmsuLogo" alt="JRMSU CCS Logo" class="w-full h-full object-contain drop-shadow-2xl" />
          </div>
        </div>
        <h1 class="text-4xl font-bold mb-2">SSAAM</h1>
        <p class="text-sm">Student School Activities Attendance Monitoring</p>
      </div>
      <div class="absolute bottom-4 left-4 right-4 text-center text-xs text-white opacity-75">
        Copyright © 2025 Powered by CCS-Creatives Committee. Chairperson: Sheen Lee
      </div>
    </div>

    <div class="w-3/5 flex items-center justify-center p-8 bg-gray-50">
      <div class="w-full max-w-md">
        <div class="mb-8 text-center">
          <h2 class="text-3xl font-bold text-purple-900 mb-4">Let's Get Started!</h2>
          <p class="text-gray-600 text-sm mb-2">You are a few clicks away from your profile.</p>
          <p class="text-gray-600 text-sm">Input your JRMSU Student ID to continue.</p>
        </div>

        <div class="bg-white rounded-2xl shadow-lg p-8">
          <div class="flex mb-6 border-b border-gray-200">
            <button class="flex-1 py-3 px-4 text-center font-medium border-b-2 border-purple-600 text-purple-600">
              Log In
            </button>
            <button @click="goToRegister" class="flex-1 py-3 px-4 text-center font-medium text-gray-500 hover:text-gray-700 flex items-center justify-center gap-1">
              <span>👤</span> Register
            </button>
          </div>

          <form @submit.prevent="handleLogin" class="space-y-6">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Student ID</label>
              <div class="relative">
                <img src="/user.svg" alt="Student ID" class="absolute left-3 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400" />
                <input v-model="studentId" type="text" placeholder="25-A-12345" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
              <div class="relative">
                <img src="/key.svg" alt="Password" class="absolute left-3 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400" />
                <input v-model="password" :type="showPassword ? 'text' : 'password'" placeholder="Your Password (Last Name)" class="w-full pl-10 pr-8 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
                <button type="button" @click="showPassword = !showPassword" class="absolute right-3 top-1/2 transform -translate-y-1/2 transition-transform duration-300 ease-in-out"
                  :class="{ 'animate-slash': showPassword }">
                  <img :src="showPassword ? '/visibility_on.svg' : '/visibility_off.svg'" alt="Toggle password" class="w-5 h-5" />
                </button>
              </div>
            </div>

            <button type="submit" :disabled="isLoading" class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center disabled:opacity-70 disabled:cursor-not-allowed">
              <span v-if="isLoading" class="flex items-center">
                <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                Logging in...
              </span>
              <span v-else class="flex items-center">
                Login <span class="ml-2">→</span>
              </span>
            </button>

            <div class="text-center text-sm text-gray-600">
              Need help? <a href="#" class="text-purple-600 hover:underline">Contact us</a>
            </div>
          </form>

          <div class="mt-6 text-center text-xs text-gray-500">
            Powered by <button @click="showDevelopersPopup = true" class="text-yellow-500 font-medium hover:text-yellow-600 cursor-pointer">CCS - Creatives Committee</button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="mobile-bg-panel md:hidden min-h-screen flex flex-col">

    <div class="text-center text-white pt-12 pb-8 px-4 relative z-10">
      <div class="w-32 h-32 mx-auto mb-4">
        <img src="/src/assets/jrmsu-logo.webp" alt="JRMSU CCS Logo" class="w-full h-full object-contain drop-shadow-2xl" />
      </div>
      <h1 class="text-4xl font-bold mb-2">SSAAM</h1>
      <p class="text-lg mb-8">Let's Get Started!</p>
      <p class="text-sm opacity-90">You are a few clicks away from your profile.</p>
      <p class="text-sm opacity-90">Input your JRMSU Student ID to continue.</p>
    </div>

    <div class="flex-1 bg-white rounded-t-3xl shadow-2xl px-6 py-8 overflow-auto">
      <div class="max-w-md mx-auto">

        <div class="flex mb-8 bg-gray-100 rounded-lg p-1">
          <button class="flex-1 py-3 px-4 text-center font-medium rounded-md bg-white text-purple-600 shadow-sm">
            Log In
          </button>
          <button @click="goToRegister" class="flex-1 py-3 px-4 text-center font-medium text-gray-500 hover:text-gray-700 flex items-center justify-center gap-1">
            <span>👤</span> Register
          </button>
        </div>

        <form @submit.prevent="handleLogin" class="space-y-6">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Student ID</label>
            <div class="relative">
              <img src="/user.svg" alt="Student ID" class="absolute left-3 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400" />
              <input v-model="studentId" type="text" placeholder="25-A-12345" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
            <div class="relative">
              <img src="/key.svg" alt="Password" class="absolute left-3 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400" />
              <input v-model="password" :type="showPassword ? 'text' : 'password'" placeholder="Your Password (Last Name)" class="w-full pl-10 pr-8 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              <button type="button" @click="showPassword = !showPassword" class="absolute right-3 top-1/2 transform -translate-y-1/2 transition-transform duration-300 ease-in-out"
                :class="{ 'animate-slash': showPassword }">
                <img :src="showPassword ? '/visibility_on.svg' : '/visibility_off.svg'" alt="Toggle password" class="w-5 h-5" />
              </button>
            </div>
          </div>

          <button type="submit" :disabled="isLoading" class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center disabled:opacity-70 disabled:cursor-not-allowed">
            <span v-if="isLoading" class="flex items-center">
              <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              Logging in...
            </span>
            <span v-else class="flex items-center">
              Login <span class="ml-2">→</span>
            </span>
          </button>

          <div class="text-center text-sm text-gray-600">
            Need help? <a href="#" class="text-purple-600 hover:underline">Contact us</a>
          </div>
        </form>

        <div class="mt-8 text-center text-xs text-gray-500">
          Powered by <button @click="showDevelopersPopup = true" class="text-yellow-500 font-medium hover:text-yellow-600 cursor-pointer">CCS - Creatives Committee</button>
        </div>

        <div class="mt-4 text-center text-xs text-gray-400">
          Copyright © 2025 Powered by CCS-Creatives Committee. Chairperson: Sheen Lee
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import jrmsuLogo from '../assets/jrmsu-logo.webp'

const router = useRouter()
const studentId = ref('')
const password = ref('')
const isLoading = ref(false)
const showDevelopersPopup = ref(false)
const showErrorNotification = ref(false)
const errorMessage = ref('')
const showPassword = ref(false)

const developers = [
  { name: 'Jullan Maglinte', initials: 'JM', role: 'Backend Dev', facebook: 'https://facebook.com/jullan.maglinte', image: '' },
  { name: 'Keith Laranjo', initials: 'KL', role: 'Backend Dev', facebook: 'https://facebook.com/kei.takun.5070', image: '' },
  { name: 'Kenzen Miñao', initials: 'KM', role: 'Frontend Dev', facebook: 'https://facebook.com/kenzen3131', image: '' },
  { name: 'Cristoph Bagabuyo', initials: 'CB', role: 'Frontend Dev', facebook: 'https://facebook.com/cristoph.bagabuyo', image: '' },
  { name: 'Mischi Jeda Elumba', initials: 'MJ', role: 'UI/UX Designer', facebook: 'https://facebook.com/mischijeda.elumba.1', image: '' }
]

onMounted(() => {
  const currentUser = localStorage.getItem('currentUser')
  if (currentUser) {
    const user = JSON.parse(currentUser)
    if (user.studentId || user.student_id) {
      router.push('/dashboard')
    }
  }
})

const handleLogin = async () => {
  isLoading.value = true
  try {
    const enteredId = studentId.value.trim();
    const enteredPass = password.value.trim().toLowerCase();

    // Check for admin user in localStorage first
    const localUsers = JSON.parse(localStorage.getItem('users') || '[]');
    const adminUser = localUsers.find(
      (u) =>
        u.role === 'admin' &&
        u.studentId === enteredId &&
        u.lastName.toLowerCase() === enteredPass
    );

    if (adminUser) {
      console.log("ADMIN LOGIN SUCCESS:", adminUser);
      localStorage.setItem("currentUser", JSON.stringify(adminUser));
      router.push("/dashboard");
      return;
    }

    // Fetch all students from API
    const response = await fetch("https://ssaam.vercel.app/students");
    const students = await response.json();

    console.log("API STUDENTS:", students);

    // Find the matching student
    const user = students.find(
      (s) =>
        s.student_id === enteredId &&
        s.last_name.toLowerCase() === enteredPass
    );

    if (user) {
      console.log("LOGIN SUCCESS:", user);
      const normalizedUser = {
        ...user,
        studentId: user.student_id,
        firstName: user.first_name,
        lastName: user.last_name,
        middleName: user.middle_name || '',
        email: user.email || '',
        rfidCode: user.rfid_code || '',
        yearLevel: user.year_level || '',
        semester: user.semester || '',
        schoolYear: user.school_year || '',
        program: user.program || '',
        role: user.role || 'student',
        image: user.photo || user.image || ''
      };
      localStorage.setItem("currentUser", JSON.stringify(normalizedUser));
      router.push("/dashboard");
      return;
    }

    errorMessage.value = "Invalid Student ID or Last Name."
    showErrorNotification.value = true
  } catch (error) {
    console.error("Login error:", error);
    errorMessage.value = "Server error. Please try again later."
    showErrorNotification.value = true
  } finally {
    isLoading.value = false
  }
};

const goToRegister = () => {
  router.push('/register')
}
</script> 