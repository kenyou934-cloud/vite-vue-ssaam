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
        <div class="text-center mb-8">
          <div class="flex items-start justify-center gap-4 mb-4">
            <div class="text-5xl">👤➕</div>
            <div class="text-left pt-2">
              <h2 class="text-2xl font-bold text-purple-900">Let's Create</h2>
              <h2 class="text-2xl font-bold text-purple-900">Your Profile!</h2>
            </div>
          </div>
          <p class="text-gray-600 text-sm italic mb-4">Please provide your basic information.</p>
          <p class="text-sm font-semibold text-purple-900">
            {{ currentStep === 1 ? 'Step 1 - Personal Information' : currentStep === 2 ? 'Step 2 - School Information' : 'Step 3 - Photo Upload' }}
          </p>
        </div>

        <div class="bg-white rounded-2xl shadow-lg p-8">
          <div class="flex mb-6 border-b border-gray-200">
            <button @click="goToLogin" class="flex-1 py-3 px-4 text-center font-medium text-gray-500 hover:text-gray-700">
              Log In
            </button>
            <button class="flex-1 py-3 px-4 text-center font-medium border-b-2 border-purple-600 text-purple-600 flex items-center justify-center gap-1">
              <span>👤</span> Register
            </button>
          </div>

          <form @submit.prevent="handleNext" class="space-y-4">

            <div v-if="currentStep === 1" class="space-y-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">First Name</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                  <input v-model="formData.firstName" type="text" placeholder="Juan" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
                </div>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Middle Name</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                  <input v-model="formData.middleName" type="text" placeholder="Dela" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" />
                </div>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Last Name</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                  <input v-model="formData.lastName" type="text" placeholder="Cruz" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
                </div>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Suffix</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                  <select v-model="formData.suffix" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white">
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
                  <input v-model="formData.email" type="email" placeholder="juandelacruz@gmail.com" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
                </div>
              </div>
              <div class="flex items-center justify-center pt-4">
                <div class="flex space-x-2">
                  <div class="w-16 h-1 bg-purple-600 rounded"></div>
                  <div class="w-16 h-1 bg-gray-300 rounded"></div>
                  <div class="w-16 h-1 bg-gray-300 rounded"></div>
                </div>
              </div>
              <button type="submit" class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
                Next <span class="ml-2">→</span>
              </button>
            </div>

            <div v-if="currentStep === 2" class="space-y-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Student ID</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                  <input v-model="formData.studentId" type="text" placeholder="25-A-12345" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
                </div>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">RFID Code</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">📡</span>
                  <input v-model="formData.rfidCode" type="text" placeholder="12345678" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
                </div>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">Year Level</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">🎓</span>
                  <select v-model="formData.yearLevel" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white" required>
                    <option value="" disabled>Select Year Level</option>
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
                  <select v-model="formData.program" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white" required>
                    <option value="" disabled>Select Program</option>
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
                    <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 text-xs">📅</span>
                    <select v-model="formData.semester" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white text-sm" required>
                      <option value="" disabled>Semester</option>
                      <option value="1st">1st</option>
                      <option value="2nd">2nd</option>
                    </select>
                  </div>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">School Year</label>
                  <div class="relative">
                    <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 text-xs">📅</span>
                    <select v-model="formData.schoolYear" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white text-sm" required>
                      <option value="" disabled>Year</option>
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
                <button type="button" @click="currentStep--" class="flex-1 bg-white border-2 border-purple-600 text-purple-600 py-3 px-6 rounded-lg font-medium hover:bg-purple-50 transition duration-300 flex items-center justify-center">
                  <span class="mr-2">←</span>Back
                </button>
                <button type="submit" class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
                  Next <span class="ml-2">→</span>
                </button>
              </div>
            </div>

            <div v-if="currentStep === 3" class="space-y-4">
              <div class="text-center">
                <div class="w-48 h-48 mx-auto mb-4 bg-gray-200 rounded-lg flex items-center justify-center overflow-hidden">
                  <img v-if="imagePreview" :src="imagePreview" class="w-full h-full object-cover" />
                  <div v-else class="flex flex-col items-center justify-center">
                    <div class="w-24 h-24 rounded-full bg-gray-400 mb-4"></div>
                    <div class="w-32 h-20 bg-gray-500 rounded-t-full"></div>
                  </div>
                </div>
                <label class="block text-sm font-medium text-gray-700 mb-4">Upload Image</label>
                <div class="relative">
                  <input type="file" @change="handleImageUpload" accept="image/*" class="hidden" id="file-upload" />
                  <label for="file-upload" class="cursor-pointer inline-flex items-center justify-center px-8 py-3 border border-gray-300 rounded-lg shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 transition duration-300">
                    <span class="mr-2">📷</span>{{ imagePreview ? 'Change Image' : 'No File Chosen' }}
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
                <button type="button" @click="currentStep--" class="flex-1 bg-white border-2 border-purple-600 text-purple-600 py-3 px-6 rounded-lg font-medium hover:bg-purple-50 transition duration-300 flex items-center justify-center">
                  <span class="mr-2">←</span>Back
                </button>
                <button type="submit" class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
                  Register <span class="ml-2">→</span>
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
  </div>

  <div class="mobile-bg-panel md:hidden min-h-screen flex flex-col">

    <div class="text-center text-white pt-12 pb-8 px-4 relative z-10">
      <div v-if="currentStep !== 3" class="w-16 h-16 mx-auto mb-4 rounded-full bg-white bg-opacity-20 flex items-center justify-center">
        <span class="text-4xl">👤+</span>
      </div>
      <h1 class="text-3xl font-bold mb-2">Let's Create</h1>
      <h2 class="text-3xl font-bold mb-4">Your Profile!</h2>
      <p class="text-sm opacity-90 italic mb-4">Please provide your basic information.</p>
      <p class="text-base font-semibold">
        {{ currentStep === 1 ? 'Step 1 - Personal Information' : currentStep === 2 ? 'Step 2 - School Information' : 'Step 3 - Photo Upload' }}
      </p>
    </div>

    <div class="flex-1 bg-white rounded-t-3xl shadow-2xl px-6 py-8 overflow-auto">
      <div class="max-w-md mx-auto">

        <div class="flex mb-8 bg-gray-100 rounded-lg p-1">
          <button @click="goToLogin" class="flex-1 py-3 px-4 text-center font-medium text-gray-500 hover:text-gray-700">
            Log In
          </button>
          <button class="flex-1 py-3 px-4 text-center font-medium rounded-md bg-white text-purple-600 shadow-sm flex items-center justify-center gap-1">
            <span>👤</span> Register
          </button>
        </div>

        <form @submit.prevent="handleNext" class="space-y-4">

          <div v-if="currentStep === 1" class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">First Name</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input v-model="formData.firstName" type="text" placeholder="Juan" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Middle Name</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input v-model="formData.middleName" type="text" placeholder="Dela" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" />
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Last Name</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input v-model="formData.lastName" type="text" placeholder="Cruz" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Suffix</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <select v-model="formData.suffix" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white">
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
                <input v-model="formData.email" type="email" placeholder="juandelacruz@gmail.com" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>
            <div class="flex items-center justify-center pt-4">
              <div class="flex space-x-2">
                <div class="w-16 h-1 bg-purple-600 rounded"></div>
                <div class="w-16 h-1 bg-gray-300 rounded"></div>
                <div class="w-16 h-1 bg-gray-300 rounded"></div>
              </div>
            </div>
            <button type="submit" class="w-full bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
              Next <span class="ml-2">→</span>
            </button>
          </div>

          <div v-if="currentStep === 2" class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Student ID</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">👤</span>
                <input v-model="formData.studentId" type="text" placeholder="25-A-12345" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">RFID Code</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">📡</span>
                <input v-model="formData.rfidCode" type="text" placeholder="12345678" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none" required />
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Year Level</label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">🎓</span>
                <select v-model="formData.yearLevel" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white" required>
                  <option value="" disabled>Select Year Level</option>
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
                <select v-model="formData.program" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white" required>
                  <option value="" disabled>Select Program</option>
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
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 text-xs">📅</span>
                  <select v-model="formData.semester" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white text-sm" required>
                    <option value="" disabled>Semester</option>
                    <option value="1st">1st</option>
                    <option value="2nd">2nd</option>
                  </select>
                </div>
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-2">School Year</label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 text-xs">📅</span>
                  <select v-model="formData.schoolYear" class="w-full pl-10 pr-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-600 focus:border-transparent outline-none appearance-none bg-white text-sm" required>
                    <option value="" disabled>Year</option>
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
              <button type="button" @click="currentStep--" class="flex-1 bg-white border-2 border-purple-600 text-purple-600 py-3 px-6 rounded-lg font-medium hover:bg-purple-50 transition duration-300 flex items-center justify-center">
                <span class="mr-2">←</span>Back
              </button>
              <button type="submit" class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
                Next <span class="ml-2">→</span>
              </button>
            </div>
          </div>

          <div v-if="currentStep === 3" class="space-y-4">
            <div class="text-center">
              <div class="w-48 h-48 mx-auto mb-4 bg-gray-200 rounded-lg flex items-center justify-center overflow-hidden">
                <img v-if="imagePreview" :src="imagePreview" class="w-full h-full object-cover" />
                <div v-else class="flex flex-col items-center justify-center">
                  <div class="w-24 h-24 rounded-full bg-gray-400 mb-4"></div>
                  <div class="w-32 h-20 bg-gray-500 rounded-t-full"></div>
                </div>
              </div>
              <label class="block text-sm font-medium text-gray-700 mb-4">Upload Image</label>
              <div class="relative">
                <input type="file" @change="handleImageUpload" accept="image/*" class="hidden" id="file-upload-mobile" />
                <label for="file-upload-mobile" class="cursor-pointer inline-flex items-center justify-center px-8 py-3 border border-gray-300 rounded-lg shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 transition duration-300">
                  <span class="mr-2">📷</span>{{ imagePreview ? 'Change Image' : 'No File Chosen' }}
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
              <button type="button" @click="currentStep--" class="flex-1 bg-white border-2 border-purple-600 text-purple-600 py-3 px-6 rounded-lg font-medium hover:bg-purple-50 transition duration-300 flex items-center justify-center">
                <span class="mr-2">←</span>Back
              </button>
              <button type="submit" class="flex-1 bg-gradient-to-r from-purple-600 to-pink-500 text-white py-3 px-6 rounded-lg font-medium hover:from-purple-700 hover:to-pink-600 transition duration-300 flex items-center justify-center">
                Register <span class="ml-2">→</span>
              </button>
            </div>
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
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'
import jrmsuLogo from '../assets/jrmsu-logo.webp'

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
  image: '',
  role: 'student'
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