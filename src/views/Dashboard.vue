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
          <div class="w-12 h-12 rounded-full bg-white bg-opacity-30 flex items-center justify-center text-2xl">
            👤
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

        <div v-if="currentUser.role === 'admin'" class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
          <div class="bg-white rounded-lg shadow-lg p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-500 text-sm font-medium">Today's Attendance</p>
                <p class="text-3xl font-bold text-purple-900 mt-2">{{ todayAttendance }}</p>
              </div>
              <div class="w-12 h-12 bg-purple-100 rounded-full flex items-center justify-center">
                <span class="text-2xl">📅</span>
              </div>
            </div>
          </div>

          <div class="bg-white rounded-lg shadow-lg p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-500 text-sm font-medium">Total Attendance Records</p>
                <p class="text-3xl font-bold text-green-600 mt-2">{{ totalAttendanceRecords }}</p>
              </div>
              <div class="w-12 h-12 bg-green-100 rounded-full flex items-center justify-center">
                <span class="text-2xl">✓</span>
              </div>
            </div>
          </div>

          <div class="bg-white rounded-lg shadow-lg p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-500 text-sm font-medium">Attendance Rate</p>
                <p class="text-3xl font-bold text-blue-600 mt-2">{{ attendanceRate }}%</p>
              </div>
              <div class="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center">
                <span class="text-2xl">📊</span>
              </div>
            </div>
          </div>
        </div>

        <div v-if="currentUser.role === 'admin'" class="bg-white rounded-lg shadow-lg p-8 mb-8">
          <h2 class="text-2xl font-bold text-purple-900 mb-6">Today's Attendance Records</h2>
          
          <div v-if="todayAttendanceList.length === 0" class="text-center py-8 text-gray-500">
            No attendance records for today
          </div>

          <div v-else class="overflow-x-auto">
            <table class="w-full border-collapse">
              <thead>
                <tr class="bg-purple-100">
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900">Student ID</th>
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900">Name</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">Program</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">Year Level</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">Check-in Time</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">Check-out Time</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="record in todayAttendanceList" :key="record.id" class="hover:bg-gray-50">
                  <td class="border border-purple-300 px-6 py-4">{{ record.studentId }}</td>
                  <td class="border border-purple-300 px-6 py-4">{{ record.studentName }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ record.program }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ record.yearLevel }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">{{ record.checkInTime }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">
                    <span v-if="record.checkOutTime">{{ record.checkOutTime }}</span>
                    <span v-else class="text-green-600 font-medium">Active</span>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="bg-white rounded-lg shadow-lg p-8">
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
const attendanceRecords = ref([])

const displayName = computed(() => {
  if (currentUser.value.role === 'admin') {
    return 'ADMIN'
  }
  if (currentUser.value.firstName && currentUser.value.lastName) {
    return `${currentUser.value.firstName} ${currentUser.value.lastName}`
  }
  return currentUser.value.name || 'User'
})

const getTodayDate = () => {
  const today = new Date()
  return today.toISOString().split('T')[0]
}

const todayAttendanceList = computed(() => {
  const today = getTodayDate()
  return attendanceRecords.value
    .filter(record => record.date === today)
    .map(record => {
      const user = users.value.find(u => u.studentId === record.studentId)
      return {
        ...record,
        studentName: user ? `${user.firstName} ${user.lastName}` : 'Unknown',
        program: user?.program || 'N/A',
        yearLevel: user?.yearLevel || 'N/A'
      }
    })
})

const todayAttendance = computed(() => {
  return todayAttendanceList.value.length
})

const totalAttendanceRecords = computed(() => {
  return attendanceRecords.value.length
})

const attendanceRate = computed(() => {
  if (users.value.length === 0) return 0
  const rate = (todayAttendance.value / users.value.length) * 100
  return Math.round(rate * 10) / 10
})

onMounted(() => {
  const user = JSON.parse(localStorage.getItem('currentUser') || '{}')
  if (!user.role && !user.studentId) {
    router.push('/')
    return
  }
  currentUser.value = user
  users.value = JSON.parse(localStorage.getItem('users') || '[]')
  attendanceRecords.value = JSON.parse(localStorage.getItem('attendance') || '[]')
  
  if (attendanceRecords.value.length === 0 && users.value.length > 0) {
    generateSampleAttendance()
  }
})

const generateSampleAttendance = () => {
  const today = getTodayDate()
  const sampleRecords = []
  const sampleStudents = users.value.slice(0, Math.min(15, users.value.length))
  
  sampleStudents.forEach((student, index) => {
    const checkInHour = 7 + Math.floor(Math.random() * 3)
    const checkInMinute = Math.floor(Math.random() * 60)
    const checkOutHour = checkInHour + 2 + Math.floor(Math.random() * 4)
    const checkOutMinute = Math.floor(Math.random() * 60)
    
    sampleRecords.push({
      id: `att-${Date.now()}-${index}`,
      studentId: student.studentId,
      date: today,
      checkInTime: `${checkInHour.toString().padStart(2, '0')}:${checkInMinute.toString().padStart(2, '0')}`,
      checkOutTime: index % 3 === 0 ? null : `${checkOutHour.toString().padStart(2, '0')}:${checkOutMinute.toString().padStart(2, '0')}`
    })
  })
  
  localStorage.setItem('attendance', JSON.stringify(sampleRecords))
  attendanceRecords.value = sampleRecords
}

const stats = computed(() => {
  const result = {
    BSCS: { '1st year': 0, '2nd year': 0, '3rd year': 0, '4th year': 0, total: 0 },
    BSIS: { '1st year': 0, '2nd year': 0, '3rd year': 0, '4th year': 0, total: 0 },
    BSIT: { '1st year': 0, '2nd year': 0, '3rd year': 0, '4th year': 0, total: 0 }
  }
  
  users.value.forEach(user => {
    if (result[user.program] && result[user.program][user.yearLevel] !== undefined) {
      result[user.program][user.yearLevel]++
      result[user.program].total++
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