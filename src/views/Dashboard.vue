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
            <img v-if="currentUser.image" :src="currentUser.image" alt="Profile" class="w-full h-full object-cover" />
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
                <img v-if="currentUser.image" :src="currentUser.image" alt="Profile Picture" class="w-full h-full object-cover" />
                <div v-else class="w-full h-full flex items-center justify-center text-6xl text-gray-400">
                  👤
                </div>
              </div>
              <p class="text-lg font-semibold text-purple-900">{{ displayName }}</p>
              <p class="text-sm text-gray-600">{{ currentUser.studentId }}</p>
            </div>
            <div class="flex-1 grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <p class="text-sm text-gray-500 font-medium">Email</p>
                <p class="text-base text-gray-900">{{ currentUser.email }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">RFID Code</p>
                <p class="text-base text-gray-900">{{ currentUser.rfidCode }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">Program</p>
                <p class="text-base text-gray-900">{{ currentUser.program }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">Year Level</p>
                <p class="text-base text-gray-900">{{ currentUser.yearLevel }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">Semester</p>
                <p class="text-base text-gray-900">{{ currentUser.semester }}</p>
              </div>
              <div>
                <p class="text-sm text-gray-500 font-medium">School Year</p>
                <p class="text-base text-gray-900">{{ currentUser.schoolYear }}</p>
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

        <div v-if="currentUser.role === 'admin'" class="bg-white rounded-lg shadow-lg p-8">
          <h2 class="text-2xl font-bold text-purple-900 mb-6">User Management</h2>

          <div class="mb-6">
            <input 
              v-model="searchQuery" 
              type="text" 
              placeholder="🔍 Search students by name, ID, email, or program..." 
              class="w-full px-4 py-3 border-2 border-purple-300 rounded-lg focus:outline-none focus:border-purple-600 focus:ring-2 focus:ring-purple-200 transition"
            />
          </div>

          <div class="overflow-x-auto">
            <table class="w-full border-collapse">
              <thead>
                <tr class="bg-purple-100">
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900">Name</th>
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900">Student ID</th>
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900">Email</th>
                  <th class="border border-purple-300 px-6 py-3 text-left font-semibold text-purple-900">Program</th>
                  <th class="border border-purple-300 px-6 py-3 text-center font-semibold text-purple-900">Actions</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="user in filteredUsers" :key="user.studentId" class="hover:bg-gray-50">
                  <td class="border border-purple-300 px-6 py-4 text-gray-700">{{ user.firstname }} {{ user.lastName }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-gray-700">{{ user.studentId }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-gray-700">{{ user.email }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-gray-700">{{ user.program }}</td>
                  <td class="border border-purple-300 px-6 py-4 text-center">
                    <button @click="openEditModal(user)" class="px-2 py-1 text-sm bg-blue-500 text-white rounded font-medium hover:bg-blue-600 transition duration-300 mr-1">
                      ✏️  
                      </button>
                    <button @click="removeUser(user.studentId)" class="px-2 py-1 text-sm bg-red-500 text-white rounded font-medium hover:bg-red-600 transition duration-300">
                      🗑️ 
                    </button>
                  </td>
                </tr>
                <tr v-if="filteredUsers.length === 0">
                  <td colspan="5" class="border border-purple-300 px-6 py-4 text-center text-gray-500">
                    {{ users.length === 0 ? 'No users registered yet.' : 'No students match your search.' }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div v-if="showEditModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
          <div class="bg-white rounded-lg shadow-2xl p-8 w-full max-w-md">
            <h3 class="text-2xl font-bold text-purple-900 mb-6">Edit User</h3>
            
            <form @submit.prevent="saveUserChanges" class="space-y-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">First Name</label>
                <input v-model="editingUser.first_name" type="text" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Last Name</label>
                <input v-model="editingUser.last_name" type="text" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
                <input v-model="editingUser.email" type="email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Program</label>
                <select v-model="editingUser.program" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white" required>
                  <option value="BSCS">BSCS</option>
                  <option value="BSIS">BSIS</option>
                  <option value="BSIT">BSIT</option>
                </select>
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Year Level</label>
                <select v-model="editingUser.yearLevel" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white" required>
                  <option value="1st year">1st year</option>
                  <option value="2nd year">2nd year</option>
                  <option value="3rd year">3rd year</option>
                  <option value="4th year">4th year</option>
                </select>
              </div>

              <div class="flex gap-4 pt-6">
                <button type="button" @click="closeEditModal" class="flex-1 px-4 py-3 border-2 border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition duration-300">
                  Cancel
                </button>
                <button type="submit" class="flex-1 px-4 py-3 bg-purple-600 text-white rounded-lg font-medium hover:bg-purple-700 transition duration-300">
                  Save Changes
                </button>
              </div>
            </form>
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
const searchQuery = ref('')

const displayName = computed(() => {
  if (currentUser.value.firstName && currentUser.value.lastName) {
    return `${currentUser.value.firstName} ${currentUser.value.lastName}`
  }
  return currentUser.value.name || 'User'
})

const filteredUsers = computed(() => {
  if (!searchQuery.value.trim()) {
    return users.value
  }
  
  const query = searchQuery.value.toLowerCase().trim()
  return users.value.filter(user => {
    const fullName = `${user.firstName} ${user.lastName}`.toLowerCase()
    const studentId = user.studentId.toLowerCase()
    const email = user.email.toLowerCase()
    const program = user.program.toLowerCase()
    
    return (
      fullName.includes(query) ||
      studentId.includes(query) ||
      email.includes(query) ||
      program.includes(query)
    )
  })
})

onMounted(() => {
  const user = JSON.parse(localStorage.getItem('currentUser') || '{}')
  if (!user.studentId) {
    router.push('/')
    return
  }
  currentUser.value = user
  users.value = JSON.parse(localStorage.getItem('users') || '[]')
})

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

const showEditModal = ref(false)
const editingUser = ref({})

const openEditModal = (user) => {
  editingUser.value = { ...user }
  showEditModal.value = true
}

const closeEditModal = () => {
  showEditModal.value = false
  editingUser.value = {}
}

const saveUserChanges = () => {
  const userIndex = users.value.findIndex(u => u.studentId === editingUser.value.studentId)
  if (userIndex !== -1) {
    users.value[userIndex] = { ...users.value[userIndex], ...editingUser.value }
    localStorage.setItem('users', JSON.stringify(users.value))
    closeEditModal()
  }
}

const removeUser = (studentId) => {
  if (confirm(`Are you sure you want to remove this user? This action cannot be undone.`)) {
    users.value = users.value.filter(user => user.studentId !== studentId)
    localStorage.setItem('users', JSON.stringify(users.value))
  }
}
</script>