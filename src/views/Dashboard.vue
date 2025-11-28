<template>
  <div v-if="showLogoutConfirmation" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50" @click.self="showLogoutConfirmation = false">
    <div class="bg-white rounded-2xl shadow-2xl p-8 max-w-sm w-full mx-4">
      <h3 class="text-2xl font-bold text-purple-900 mb-4">Confirm Logout</h3>
      <p class="text-gray-600 mb-6">Are you sure you want to exit? You'll be logged out of your account.</p>
      <div class="flex gap-3">
        <button @click="showLogoutConfirmation = false" class="flex-1 bg-gray-200 text-gray-800 py-2 px-4 rounded-lg font-medium hover:bg-gray-300 transition">
          Cancel
        </button>
        <button @click="confirmLogout" class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-2 px-4 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition">
          Logout
        </button>
      </div>
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

  <div v-if="isPageLoading" class="fixed inset-0 bg-gradient-to-b from-purple-600 to-pink-400 flex items-center justify-center z-50">
    <div class="text-center text-white">
      <svg class="animate-spin h-16 w-16 mx-auto mb-4" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
      </svg>
      <p class="text-xl font-semibold">Loading Dashboard...</p>
      <p class="text-sm opacity-75 mt-2">Please wait while we fetch your data</p>
    </div>
  </div>

  <div v-else class="flex h-screen flex-col md:flex-row">
    <div class="w-full md:w-64 bg-gradient-to-b from-purple-600 to-pink-400 text-white flex flex-col order-2 md:order-1 border-t-2 md:border-t-0 md:border-r-2 border-white border-opacity-20">
      <div class="p-6 border-b border-white border-opacity-20">
        <div class="flex items-center justify-center mb-2">
          <img src="/src/assets/jrmsu-logo.webp" alt="JRMSU CCS Logo" class="w-32 h-32 object-contain drop-shadow-xl" />
        </div>
        <h1 class="text-xl font-bold text-center">SSAAM</h1>
      </div>

      <div class="p-6 border-b border-white border-opacity-20">
        <div class="flex items-center space-x-3">
          <div class="w-12 h-12 rounded-full bg-white bg-opacity-30 flex items-center justify-center text-2xl overflow-hidden">
            <div v-if="sidebarImageLoading" class="w-full h-full flex items-center justify-center">
              <svg class="animate-spin h-6 w-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
            </div>
            <img v-else-if="currentUser.image || currentUser.photo" :src="currentUser.image || currentUser.photo" alt="Profile" class="w-full h-full object-cover" @load="sidebarImageLoading = false" @error="sidebarImageLoading = false" />
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
        <button @click="showDevelopersPopup = true" class="text-yellow-300 hover:text-yellow-400 cursor-pointer">CCS - Creatives Committee</button>
      </div>
    </div>

    <div class="flex-1 bg-gray-100 overflow-auto order-1 md:order-2">
      <div class="p-4 md:p-8">
        <h1 class="text-2xl md:text-4xl font-bold text-purple-900 mb-8 pb-4 border-b-2 border-purple-900">Dashboard</h1>

        <div v-if="currentUser.role !== 'admin'" class="bg-white rounded-lg shadow-lg p-4 md:p-8 mb-8">
          <h2 class="text-xl md:text-2xl font-bold text-purple-900 mb-6">My Profile</h2>
          <div class="flex flex-col gap-8">
            <div class="flex flex-col items-center">
              <div class="w-32 h-32 rounded-full bg-gray-200 overflow-hidden mb-4 shadow-lg">
                <div v-if="profileImageLoading" class="w-full h-full flex items-center justify-center bg-purple-100">
                  <svg class="animate-spin h-10 w-10 text-purple-600" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                  </svg>
                </div>
                <img v-else-if="currentUser.image || currentUser.photo" :src="currentUser.image || currentUser.photo" alt="Profile Picture" class="w-full h-full object-cover" @load="profileImageLoading = false" @error="profileImageLoading = false" />
                <div v-else class="w-full h-full flex items-center justify-center text-6xl text-gray-400">
                  👤
                </div>
              </div>
              <p class="text-lg font-semibold text-purple-900">{{ displayName }}</p>
              <p class="text-sm text-gray-600">{{ currentUser.studentId || currentUser.student_id }}</p>
            </div>
            <div class="flex-1 grid grid-cols-1 sm:grid-cols-2 gap-4">
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

        <div v-if="currentUser.role === 'admin'" class="bg-white rounded-lg shadow-lg p-4 md:p-8 mb-8">
          <h2 class="text-xl md:text-2xl font-bold text-purple-900 mb-6">Registered Students</h2>

          <div class="overflow-x-auto text-sm md:text-base">
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
const isPageLoading = ref(true)
const profileImageLoading = ref(false)
const sidebarImageLoading = ref(false)
const showDevelopersPopup = ref(false)
const showLogoutConfirmation = ref(false)

const developers = [
  { name: 'Jullan Maglinte', initials: 'JM', role: 'Backend Dev', facebook: 'https://facebook.com', image: '' },
  { name: 'Keith Laranjo', initials: 'KL', role: 'Backend Dev', facebook: 'https://facebook.com', image: '' },
  { name: 'Kenzen Miñao', initials: 'KM', role: 'Frontend Dev', facebook: 'https://facebook.com', image: '' },
  { name: 'Cristoph Bagabuyo', initials: 'CB', role: 'Frontend Dev', facebook: 'https://facebook.com', image: '' },
  { name: 'Mischi Jeda Elumba', initials: 'MJ', role: 'UI/UX Designer', facebook: 'https://facebook.com', image: '' }
]

const displayName = computed(() => {
  const firstName = currentUser.value.firstName || currentUser.value.first_name
  const lastName = currentUser.value.lastName || currentUser.value.last_name
  if (currentUser.value.role === 'admin') {
    return firstName || 'Administrator'
  }
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
  
  // Hide page loading after data is fetched
  isPageLoading.value = false
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
  showLogoutConfirmation.value = true
}

const confirmLogout = () => {
  showLogoutConfirmation.value = false
  localStorage.removeItem('currentUser')
  router.push('/')
}
</script>