<template>
  <section class="w-full bg-couples bg-cover h-screen">
    <section class="container-section h-screen grid content-end">
      <!-- Form Generator Link -->
      <div v-if="showLinkGenerator" class="fixed top-0 left-0 w-full h-full bg-black bg-opacity-70 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded-lg w-11/12 max-w-md">
          <h2 class="text-xl font-bold mb-4 text-gray-800">Generator Link Undangan</h2>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm mb-2">Nama Tamu</label>
            <input 
              v-model="guestName" 
              type="text" 
              class="w-full px-3 py-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-orange-200"
              placeholder="Masukkan nama tamu">
          </div>
          <div v-if="generatedLink" class="mb-4">
            <label class="block text-gray-700 text-sm mb-2">Link Undangan:</label>
            <div class="flex">
              <input 
                type="text" 
                readonly 
                :value="generatedLink" 
                class="w-full px-3 py-2 border border-gray-300 rounded-l focus:outline-none">
              <button 
                @click="copyToClipboard" 
                class="bg-amber-500 text-white px-4 rounded-r hover:bg-amber-600">
                Copy
              </button>
            </div>
            <p v-if="copySuccess" class="text-green-600 text-sm mt-1">Link berhasil disalin!</p>
          </div>
          <div class="flex justify-between">
            <button 
              @click="generateLink" 
              class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
              Generate Link
            </button>
            <button 
              @click="showLinkGenerator = false" 
              class="bg-gray-300 text-gray-800 px-4 py-2 rounded hover:bg-gray-400">
              Tutup
            </button>
          </div>
        </div>
      </div>
      
      <!-- Button to open generator -->
      <button 
        v-if="!showLinkGenerator && !hasGuestParameter" 
        @click="showLinkGenerator = true"
        class="fixed bottom-5 right-5 bg-orange-500 text-white p-3 rounded-full shadow-lg z-10 hover:bg-orange-600">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
        </svg>
      </button>
      
      <!-- Undangan Content -->
      <div 
        class="animate__animated animate__fadeInUpBig text-gray-100 text-center bg-amber-700 bg-opacity-50 backdrop-blur-sm rounded-t-3xl px-6 py-10">
        <p>Pernikahan</p>
        <h1 class="tangerine-font text-title font-bold">{{ couples.join(' & ') }}</h1>
        <decoration class="fill-amber-400 mx-auto w-3/12 mb-3"></decoration>
        <p class="text-sm">
          <p class="font-medium">Kepada Bapak/Ibu/Saudara/i Yang Terhormat</p>
          <p class="font-medium my-2 text-lg">{{ query.to }}</p>
          <small>Izinkan kami turut mengundang anda dalam acara kami</small>
        </p>
      </div>
    </section>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'
import decoration from '@/assets/svg/decoration-2.svg'

const couples = ['Akmal', 'Reva']
const route = useRoute()
const query = computed(() => route.query.to ? route.query : { to: 'Saudara/i' })
const hasGuestParameter = computed(() => route.query.to && route.query.to !== 'Saudara/i')

// Link generator functionality
const showLinkGenerator = ref(false)
const guestName = ref('')
const generatedLink = ref('')
const copySuccess = ref(false)

const generateLink = () => {
  if (!guestName.value.trim()) return
  
  const baseUrl = window.location.origin + window.location.pathname
  generatedLink.value = `${baseUrl}?to=${encodeURIComponent(guestName.value.trim())}`
}

const copyToClipboard = () => {
  navigator.clipboard.writeText(generatedLink.value)
    .then(() => {
      copySuccess.value = true
      setTimeout(() => copySuccess.value = false, 2000)
    })
}
</script>