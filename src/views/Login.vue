<template>
  <div class="hidden md:flex min-h-screen bg-white">
    <div class="desktop-bg-panel">
      <div class="relative z-10 text-center">
        <div class="mb-4">
          <div class="w-40 h-40 mx-auto flex items-center justify-center">
            <img :src="jrmsuLogo" alt="JRMSU CCS Logo" class="w-full h-full object-contain drop-shadow-2xl" />
          </div>
        </div>
        <h1 class="text-4xl font-bold mb-2">SSAAM LOGO</h1>
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
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input v-model="studentId" type="text" placeholder="25-A-12345" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">🔑</span>
                <input v-model="password" type="password" placeholder="Your Password (Last Name)" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>

            <button type="submit" class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
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
  </div>

  <div class="mobile-bg-panel md:hidden min-h-screen flex flex-col">

    <div class="text-center text-white pt-12 pb-8 px-4 relative z-10">
      <div class="w-32 h-32 mx-auto mb-4">
        <img src="/src/assets/jrmsu-logo.webp" alt="JRMSU CCS Logo" class="w-full h-full object-contain drop-shadow-2xl" />
      </div>
      <h1 class="text-4xl font-bold mb-2">SSAAM LOGO</h1>
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
              <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
              <input v-model="studentId" type="text" placeholder="25-A-12345" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
            <div class="relative">
              <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">🔑</span>
              <input v-model="password" type="password" placeholder="Your Password (Last Name)" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
            </div>
          </div>

          <button type="submit" class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
            Login
            <span class="ml-2">→</span>
          </button>

          <div class="text-center text-sm text-gray-600">
            Need help? <a href="#" class="text-purple-600 hover:underline">Contact us</a>
          </div>
        </form>

        <div class="mt-8 text-center text-xs text-gray-500">
          Powered by <span class="text-yellow-500 font-medium">CCS - Creatives Committee</span>
        </div>

        <div class="mt-4 text-center text-xs text-gray-400">
          Copyright © 2025 Powered by CCS-Creatives Committee. Chairperson: Sheen Lee
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import jrmsuLogo from '../assets/jrmsu-logo.webp'

const router = useRouter()
const studentId = ref('')
const password = ref('')

const handleLogin = async () => {
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

    alert("Invalid Student ID or Last Name.");
  } catch (error) {
    console.error("Login error:", error);
    alert("Server error. Try again later.");
  }
};

const goToRegister = () => {
  router.push('/register')
}
</script> 