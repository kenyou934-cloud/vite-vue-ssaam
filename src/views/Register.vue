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
          <div class="flex items-center justify-center mb-4">
            <div class="w-12 h-12 rounded-full bg-purple-700 flex items-center justify-center text-white text-2xl">
              👤+
            </div>
          </div>
          <h2 class="text-3xl font-bold text-purple-900 mb-2">Let's Create</h2>
          <h2 class="text-3xl font-bold text-purple-900 mb-4">Your Profile!</h2>
          <p class="text-gray-600 text-sm italic">Please provide your basic information.</p>
        </div>

        <div class="mb-6">
          <h3 class="text-center font-semibold text-purple-900">
            {{ currentStep === 1 ? 'Step 1 - Personal Information' : currentStep === 2 ? 'Step 2 - School Information' : 'Step 3 - Profile Image' }}
          </h3>
        </div>

        <div class="flex mb-6 border-b border-gray-200">
          <button 
            @click="goToLogin"
            class="flex-1 py-3 px-4 text-center font-medium text-gray-500 hover:text-gray-700"
          >
            Log In
          </button>
          <button 
            class="flex-1 py-3 px-4 text-center font-medium border-b-2 border-purple-600 text-purple-600"
          >
            👤 Register
          </button>
        </div>

        <form @submit.prevent="handleNext" class="space-y-4">
          <div v-if="currentStep === 1" class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">First Name</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input
                  v-model="formData.firstName"
                  type="text"
                  placeholder="Juan"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                  required
                />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Middle Name</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input
                  v-model="formData.middleName"
                  type="text"
                  placeholder="Dela"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Last Name</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input
                  v-model="formData.lastName"
                  type="text"
                  placeholder="Cruz"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                  required
                />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Suffix</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <select
                  v-model="formData.suffix"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none"
                >
                  <option value="">Select Suffix</option>
                  <option value="Jr.">Jr.</option>
                  <option value="Sr.">Sr.</option>
                  <option value="II">II</option>
                  <option value="III">III</option>
                  <option value="IV">IV</option>
                </select>
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">E-mail</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">✉️</span>
                <input
                  v-model="formData.email"
                  type="email"
                  placeholder="juandelacruz@gmail.com"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                  required
                />
              </div>
            </div>

            <div class="flex items-center justify-center pt-4">
              <div class="flex space-x-2">
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
                <div class="w-16 h-1 bg-gray-300 rounded"></div>
                <div class="w-16 h-1 bg-gray-300 rounded"></div>
              </div>
            </div>

            <button
              type="submit"
              class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center"
            >
              Next
              <span class="ml-2">→</span>
            </button>
          </div>

          <div v-if="currentStep === 2" class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Student ID</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input
                  v-model="formData.studentId"
                  type="text"
                  placeholder="25-A-12345"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                  required
                />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">RFID Code</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">📡</span>
                <input
                  v-model="formData.rfidCode"
                  type="text"
                  placeholder="12345678"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none"
                  required
                />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Year Level</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">🎓</span>
                <select
                  v-model="formData.yearLevel"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none"
                  required
                >
                  <option value="">Select Year Level</option>
                  <option value="1st year">1st year</option>
                  <option value="2nd year">2nd year</option>
                  <option value="3rd year">3rd year</option>
                  <option value="4th year">4th year</option>
                </select>
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Program</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">📚</span>
                <select
                  v-model="formData.program"
                  class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none"
                  required
                >
                  <option value="">Select Program</option>
                  <option value="BSCS">BSCS</option>
                  <option value="BSIS">BSIS</option>
                  <option value="BSIT">BSIT</option>
                </select>
              </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Semester</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">📅</span>
                  <select
                    v-model="formData.semester"
                    class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none"
                    required
                  >
                    <option value="">Semester</option>
                    <option value="1st">1st</option>
                    <option value="2nd">2nd</option>
                  </select>
                </div>
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">School Year</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">📅</span>
                  <select
                    v-model="formData.schoolYear"
                    class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none"
                    required
                  >
                    <option value="">Year</option>
                    <option value="2024-2025">2024-2025</option>
                    <option value="2025-2026">2025-2026</option>
                  </select>
                </div>
              </div>
            </div>

            <div class="flex items-center justify-center pt-4">
              <div class="flex space-x-2">
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
                <div class="w-16 h-1 bg-gray-300 rounded"></div>
              </div>
            </div>

            <div class="flex gap-4">
              <button
                type="button"
                @click="currentStep--"
                class="flex-1 bg-white border-2 border-purple-600 text-purple-600 py-3 px-6 rounded-lg font-medium hover:bg-purple-50 transition duration-300 flex items-center justify-center"
              >
                <span class="mr-2">←</span>
                Back
              </button>
              <button
                type="submit"
                class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center"
              >
                Next
                <span class="ml-2">→</span>
              </button>
            </div>
          </div>

          <div v-if="currentStep === 3" class="space-y-4">
            <div class="text-center">
              <div class="w-48 h-48 mx-auto mb-4 bg-gray-200 rounded-lg flex items-center justify-center overflow-hidden">
                <img v-if="imagePreview" :src="imagePreview" class="w-full h-full object-cover" />
                <div v-else class="text-gray-400 text-6xl">👤</div>
              </div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Upload Image</label>
              <div class="relative">
                <input
                  type="file"
                  @change="handleImageUpload"
                  accept="image/*"
                  class="hidden"
                  id="file-upload"
                />
                <label
                  for="file-upload"
                  class="cursor-pointer inline-flex items-center px-6 py-3 border border-gray-300 rounded-lg shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50"
                >
                  📷 {{ imagePreview ? 'Change Image' : 'No File Chosen' }}
                </label>
              </div>
            </div>

            <div class="flex items-center justify-center pt-4">
              <div class="flex space-x-2">
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
              </div>
            </div>

            <div class="flex gap-4">
              <button
                type="button"
                @click="currentStep--"
                class="flex-1 bg-white border-2 border-purple-600 text-purple-600 py-3 px-6 rounded-lg font-medium hover:bg-purple-50 transition duration-300 flex items-center justify-center"
              >
                <span class="mr-2">←</span>
                Back
              </button>
              <button
                type="submit"
                class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center"
              >
                Register
                <span class="ml-2">→</span>
              </button>
            </div>
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
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const currentStep = ref(1)
const imagePreview = ref('')

const formData = reactive({
  firstName: '',
  middleName: '',
  lastName: '',
  suffix: '',
  email: '',
  studentId: '',
  rfidCode: '',
  yearLevel: '',
  program: '',
  semester: '',
  schoolYear: '',
  image: ''
})

const handleImageUpload = (event) => {
  const file = event.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = (e) => {
      imagePreview.value = e.target.result
      formData.image = e.target.result
    }
    reader.readAsDataURL(file)
  }
}

const handleNext = () => {
  if (currentStep.value < 3) {
    currentStep.value++
  } else {
    const users = JSON.parse(localStorage.getItem('users') || '[]')
    users.push({ ...formData })
    localStorage.setItem('users', JSON.stringify(users))
    alert('Registration successful! Please login.')
    router.push('/')
  }
}

const goToLogin = () => {
  router.push('/')
}
</script>