<template>
  <div class="flex h-screen">
    <div class="w-64 bg-gradient-to-b from-purple-600 to-pink-400 text-white flex flex-col">
      <div class="p-6 border-b border-white border-opacity-20">
        <div class="flex items-center justify-center mb-2">
          <img src="/src/assets/jrmsu-logo.webp" alt="JRMSU CCS Logo" class="w-32 h-32 object-contain drop-shadow-xl" />
        </div>
        <h1 class="text-xl font-bold text-center">SSAAM</h1>
      </div>

      <div class="p-6 border-b border-white border-opacity-20">
        <div class="flex items-center space-x-3">
          <div class="w-12 h-12 rounded-full bg-white bg-opacity-30 flex items-center justify-center text-2xl overflow-hidden">
            <img v-if="currentUser.image || currentUser.photo" :src="currentUser.image || currentUser.photo" alt="Profile" class="w-full h-full object-cover" />
            <span v-else>👤</span>
          </div>
          <div>
            <p class="text-sm">Welcome back,</p>
            <p class="font-bold">{{ displayName }}!</p>
          </div>
        </div>
      </div>

      <nav class="flex-1 p-4">
        <a href="#" class="flex items-center space-x-3 px-4 py-3 rounded-lg bg-white bg-opacity-20 mb-2">
          <span>🏠</span>
          <span>Dashboard</span>
        </a>
        <button 
          @click="handleLogout"
          class="flex items-center space-x-3 px-4 py-3 rounded-lg hover:bg-white hover:bg-opacity-10 w-full text-left"
        >
          <span>🚪</span>
          <span>Log Out</span>
        </button>
      </nav>

      <div class="p-4 text-xs text-white opacity-75">
        <p>Powered by</p>
        <p class="text-yellow-300">CCS - Creatives Committee</p>
      </div>
    </div>

    <div class="flex-1 bg-gray-100 overflow-auto">
      <div class="p-8">
        <h1 class="text-4xl font-bold text-purple-900 mb-8 pb-4 border-b-2 border-purple-900">Dashboard</h1>

        <div v-if="currentUser.role !== 'admin'" class="bg-white rounded-lg shadow-lg p-8 mb-8">
          <h2 class="text-2xl font-bold text-purple-900 mb-6">My Profile</h2>
          <div class="flex flex-col md:flex-row gap-8">
            <div class="flex flex-col items-center">
              <div class="w-32 h-32 rounded-full bg-gray-200 overflow-hidden mb-4 shadow-lg">
                <img v-if="currentUser.image || currentUser.photo" :src="currentUser.image || currentUser.photo" alt="Profile Picture" class="w-full h-full object-cover" />
                <div v-else class="w-full h-full flex items-center justify-center text-6xl text-gray-400">
                  👤
                </div>
              </div>
              <p class="text-lg font-semibold text-purple-900">{{ displayName }}</p>
              <p class="text-sm text-gray-600">{{ currentUser.studentId || currentUser.student_id }}</p>
            </div>
            <div class="flex-1 grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <p class="text-sm text-gray-500 font-medium">Email</p>
                <p class="text-base text-gray-900">{{ currentUser.email || 'Not provided' }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">RFID Code</p>
                <p class="text-base text-gray-900">{{ currentUser.rfidCode || currentUser.rfid_code || 'Not provided' }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">Program</p>
                <p class="text-base text-gray-900">{{ currentUser.program || 'Not provided' }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">Year Level</p>
                <p class="text-base text-gray-900">{{ currentUser.yearLevel || currentUser.year_level || 'Not provided' }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">Semester</p>
                <p class="text-base text-gray-900">{{ currentUser.semester || 'Not provided' }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">School Year</p>
                <p class="text-base text-gray-900">{{ currentUser.schoolYear || currentUser.school_year || 'Not provided' }}</p>
              </div>
            </div>
          </div>
        </div>

        <div v-if="currentUser.role === 'admin'" class="bg-white rounded-lg shadow-lg p-8 mb-8">
          <h2 class="text-2xl font-bold text-purple-900 mb-6">Registered Students</h2>

          <div class="overflow-x-auto">
            <table class="w-full border-collapse">
              <thead>
                <tr class="bg-purple-100">
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900"></th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">BSCS</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">BSIS</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">BSIT</th>
                </tr>
              </thead>
              <tbody>
                <tr class="hover:bg-gray-50">
                  <td class="border border-purple-300 px-6 py-4 font-medium text-gray-700">1st years</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSCS['1st year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIS['1st year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIT['1st year'] }}</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="border border-purple-300 px-6 py-4 font-medium text-gray-700">2nd years</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSCS['2nd year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIS['2nd year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIT['2nd year'] }}</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="border border-purple-300 px-6 py-4 font-medium text-gray-700">3rd years</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSCS['3rd year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIS['3rd year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIT['3rd year'] }}</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="border border-purple-300 px-6 py-4 font-medium text-gray-700">4th years</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSCS['4th year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIS['4th year'] }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIT['4th year'] }}</td>
                </tr>
                <tr class="bg-purple-50 font-bold">
                  <td class="border border-purple-300 px-6 py-4 font-bold text-gray-900">All year levels</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSCS.total }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIS.total }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ stats.BSIT.total }}</td>
                </tr>
              </tbody>
            </table>
          </div>

          <div class="mt-6 text-center">
            <p class="text-lg font-semibold text-purple-900">
              Total Registered Students: <span class="text-2xl">{{ totalStudents }}</span>
            </p>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const currentUser = ref({})
const users = ref([])

const displayName = computed(() => {
  const firstName = currentUser.value.firstName || currentUser.value.first_name
  const lastName = currentUser.value.lastName || currentUser.value.last_name
  if (firstName && lastName) {
    return `${firstName} ${lastName}`
  }
  return currentUser.value.name || 'User'
})

onMounted(async () => {
  const user = JSON.parse(localStorage.getItem('currentUser') || '{}')
  if (!user.studentId && !user.student_id) {
    router.push('/')
    return
  }
  currentUser.value = user
  
  // If admin, fetch students from API
  if (user.role === 'admin') {
    try {
      const response = await fetch('https://ssaam.vercel.app/students')
      const apiStudents = await response.json()
      // Normalize API data to match expected field names
      users.value = apiStudents.map(s => ({
        ...s,
        studentId: s.student_id,
        firstName: s.first_name,
        lastName: s.last_name,
        yearLevel: s.year_level,
        rfidCode: s.rfid_code,
        schoolYear: s.school_year,
        image: s.photo || s.image || ''
      }))
    } catch (error) {
      console.error('Failed to fetch students:', error)
      users.value = []
    }
  } else {
    users.value = JSON.parse(localStorage.getItem('users') || '[]')
  }
})

const stats = computed(() => {
  const result = {
    BSCS: { '1st year': 0, '2nd year': 0, '3rd year': 0, '4th year': 0, total: 0 },
    BSIS: { '1st year': 0, '2nd year': 0, '3rd year': 0, '4th year': 0, total: 0 },
    BSIT: { '1st year': 0, '2nd year': 0, '3rd year': 0, '4th year': 0, total: 0 }
  }
  
  users.value.forEach(user => {
    const program = user.program
    const yearLevel = user.yearLevel || user.year_level
    if (result[program] && result[program][yearLevel] !== undefined) {
      result[program][yearLevel]++
      result[program].total++
    }
  })
  
  return result
})

const totalStudents = computed(() => {
  return stats.value.BSCS.total + stats.value.BSIS.total + stats.value.BSIT.total
})

const handleLogout = () => {
  localStorage.removeItem('currentUser')
  router.push('/')
}
</script>