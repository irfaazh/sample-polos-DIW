<template>
  <section class="w-full bg-gradient-to-b from-orange-100 to-orange-50 pt-5 pb-8">
    <!-- Form Section -->
    <section class="container-section bg-gradient-to-b from-orange-50 to-orange-100 p-5 rounded-lg shadow-md mx-auto w-11/12 max-w-md">
      <!-- Header dengan ornamen -->
      <div class="text-center mb-6">
        <h1 class="satisfy-font text-4xl font-medium mb-5 text-amber-800">Buku Tamu</h1>
        <p class="text-sm text-amber-700 mt-2">Demi kelancaran acara dimohon untuk para tamu undangan untuk memastikan kehadirannya pada acara kami</p>
      </div>
      
      <!-- Form -->
      <form 
        ref="form"
        @submit="sendMessage"
        class="w-full mx-auto">
        <!-- Alert -->
        <Alert v-if="showAlert" :statusResponse="statusResponse" :showAlert="showAlert" v-on:close="showAlert = false" />
        
        <!-- Guest Name -->
        <div class="input-wrapper" data-aos="zoom-in">
          <label for="GuestName">Nama</label>
          <input v-model="GuestName" placeholder="Nama lengkap anda" name="GuestName" id="GuestName" type="text" required>
        </div>
        
        <!-- Guest Status -->
        <div class="input-wrapper" data-aos="zoom-in">
          <label for="GuestStatus">Kehadiran</label>
          <select v-model="GuestStatus" name="GuestStatus" id="GuestStatus" required>
            <option value="Hadir">Hadir</option>
            <option value="Tidak Hadir">Tidak Hadir</option>
          </select>
        </div>
        
        <!-- Guest Message -->
        <div class="input-wrapper" data-aos="zoom-in">
          <label for="GuestMessage">Pesan</label>
          <textarea placeholder="Tuliskan pesan anda disini" v-model="GuestMessage" name="GuestMessage" id="GuestMessage" cols="30" rows="5" required></textarea>
        </div>
        
        <!-- Submit Button -->
        <button 
          data-aos="zoom-in"
          class="w-full bg-orange-800 text-orange-100 mt-6 rounded-lg py-3 font-medium cursor-pointer active:scale-95 hover:border hover:border-orange-500 hover:bg-orange-100 hover:text-amber-800 duration-300" 
          type="submit">
          <i class="fa fa-paper-plane mr-1"></i>
          Kirim pesan
        </button>
      </form>
    </section>
    
    <!-- Messages Section -->
    <MessagesBox :messages="messages" />
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import Alert from '@/components/Alert.vue'
import MessagesBox from '@/components/MessagesBox.vue'

const scriptURL = "https://script.google.com/macros/s/AKfycbzrE11My5dfOO7WwjwMbyjMsVuyo1osZa8vYiFJxP16CyMNXEZNjVjkqmq8YGRpUt8v/exec"

// Form refs
const form = ref(null)
const GuestName = ref('')
const GuestMessage = ref('')
const GuestStatus = ref('Hadir')

// Alert state
const statusResponse = ref(false)
const showAlert = ref(false)

// Messages data
const messages = ref([])

// Form submission
const sendMessage = async (evt) => {
  evt.preventDefault()
  
  try {
    const res = await fetch(scriptURL, { method: 'POST', body: new FormData(form.value) })
    statusResponse.value = true
    showAlert.value = true
    await fetchMessages()
    GuestName.value = ''
    GuestMessage.value = ''
    GuestStatus.value = 'Hadir'
  } catch (err) {
    console.error('Error:', err)
    statusResponse.value = false
    showAlert.value = true
  }
}

// Fetch messages
const fetchMessages = async () => {
  try {
    const res = await fetch(scriptURL)
    messages.value = (await res.json()).reverse()
  } catch (error) {
    console.error('Error fetching messages:', error)
  }
}

// Auto-fill guest name from URL
const route = useRoute()
if (route.query.to) GuestName.value = route.query.to

// Initial fetch
onMounted(fetchMessages)
</script>

<style scoped>
.container-section {
  max-width: 500px;
}

.input-wrapper {
  @apply w-full flex flex-col gap-2 mb-4;
}

label {
  @apply text-orange-800 font-medium text-sm;
}

input, textarea, select {
  @apply w-full px-3 py-3 rounded-lg bg-orange-800 border border-amber-600 shadow-md focus:outline-none focus:ring-2 focus:ring-amber-50 text-amber-50 placeholder:text-amber-50 transition duration-300;
}

textarea {
  min-height: 100px;
  resize: vertical;
}

button {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

button:hover {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}
</style>