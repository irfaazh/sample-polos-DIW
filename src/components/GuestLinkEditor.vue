<template>
    <section class="max-w-3xl mx-auto p-6 space-y-6">
      <h2 class="text-2xl font-bold mb-4">Daftar Tamu & Link Undangan</h2>
  
      <!-- FORM -->
      <div v-for="(guest, index) in guests" :key="index" class="flex flex-col md:flex-row md:items-center gap-2 mb-3">
        <input
          v-model="guest.name"
          type="text"
          class="flex-1 p-2 rounded-md bg-orange-200  bg-orange-200 text-orange-50 focus:text-red-800 placeholder-orange-800"
          placeholder="Nama tamu"
        />
  
        <button
          @click="copyLink(guest)"
          class="bg-orange-700 hover:bg-orange-800 text-orange-50 px-3 py-1 rounded text-sm"
        >
          Salin Link
        </button>
  
        <button
          @click="removeGuest(index)"
          class="text-red-600 hover:underline text-sm"
        >
          Hapus
        </button>
      </div>
  
      <!-- BUTTON TAMBAH -->
      <button
        @click="addGuest"
        class="bg-orange-700 hover:bg-orange-800 text-orange-50 px-4 py-2 rounded"
      >
        + Tambah Tamu
      </button>
  
      <!-- NOTIF COPY -->
      <p v-if="copiedName" class="text-orange-600 font-medium mt-4">
        Link untuk "{{ copiedName }}" berhasil disalin!
      </p>
    </section>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const guests = ref([
    { name: '' }
  ])
  
  const baseUrl = 'https://undangan-pernikahan-ar.vercel.app'
  const copiedName = ref('')
  
  const addGuest = () => {
    guests.value.push({ name: '' })
  }
  
  const removeGuest = (index) => {
    guests.value.splice(index, 1)
  }
  
  const copyLink = (guest) => {
    const url = `${baseUrl}?to=${encodeURIComponent(guest.name)}`
    navigator.clipboard.writeText(url).then(() => {
      copiedName.value = guest.name
      setTimeout(() => (copiedName.value = ''), 2500)
    })
  }
  </script>
  