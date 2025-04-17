<template>
    <div class="min-h-screen bg-orange-50 p-4">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-3xl font-bold text-orange-800 mb-6">Admin Panel - Undangan Pernikahan</h1>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div>
            <h2 class="text-xl font-semibold text-orange-700 mb-4">Kelola Tamu Undangan</h2>
            <guest-manager />
          </div>
          
          <div class="bg-white p-6 rounded-lg shadow">
            <h2 class="text-xl font-semibold text-orange-700 mb-4">Pratinjau Undangan</h2>
            <div class="mb-4">
              <label class="block text-gray-700 mb-2">Nama Tamu (untuk pratinjau):</label>
              <input 
                v-model="previewGuestName" 
                type="text" 
                class="w-full p-2 border border-gray-300 rounded"
                placeholder="Masukkan nama tamu"
              />
            </div>
            
            <div class="mt-4">
              <p class="text-sm text-gray-600 mb-2">Link Pratinjau:</p>
              <div class="flex">
                <input 
                  type="text" 
                  readonly 
                  :value="previewLink" 
                  class="flex-1 p-2 border border-gray-300 rounded-l bg-gray-50"
                />
                <button 
                  @click="copyPreviewLink"
                  class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-r"
                >
                  Salin
                </button>
              </div>
              <p v-if="notification" class="text-green-600 text-sm mt-2">{{ notification }}</p>
            </div>
            
            <div class="mt-6">
              <a :href="previewLink" target="_blank" class="bg-orange-600 hover:bg-orange-700 text-white px-4 py-2 rounded inline-block">
                Lihat Pratinjau
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  import GuestManager from './GuestManager.vue'
  
  const previewGuestName = ref('Tamu Spesial')
  const notification = ref('')
  
  const baseUrl = window.location.origin + window.location.pathname
  
  const previewLink = computed(() => {
    return `${baseUrl}?to=${encodeURIComponent(previewGuestName.value)}`
  })
  
  const copyPreviewLink = () => {
    navigator.clipboard.writeText(previewLink.value)
      .then(() => {
        notification.value = 'Link berhasil disalin!'
        setTimeout(() => {
          notification.value = ''
        }, 3000)
      })
  }
  </script>