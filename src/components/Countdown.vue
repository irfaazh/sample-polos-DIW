<template>
  <div class="px-2 py-4">
    <p class="mx-auto text-center text-sm text-orange-50 w-10/12 mb-2">
      Menuju acara resepsi kami
    </p>

    <section v-if="!finished" class="flex justify-center gap-3">
      <template v-for="(value, name, index) in countdown" :key="index">
        <div 
          data-aos="zoom-in"
          class="text-center w-3/12">
          <p class="text-3xl font-medium text-amber-50 mb-2">{{ value }}</p>
          <p class="text-orange-50 text-sm font-medium">{{ name }}</p>
        </div>
      </template>
    </section>

    <div v-else class="text-center text-orange-50 text-lg font-semibold mt-4">
      Waktu resepsi telah tiba!
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const countdown = ref(null)
const finished = ref(false)
let timer = null

// Fungsi hitung mundur
const createTimer = (target, container, onFinish) => {
  const now = new Date().getTime()
  const distance = target - now

  if (distance > 0) {
    const days = Math.floor(distance / (1000 * 60 * 60 * 24))
    const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
    const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60))
    const seconds = Math.floor((distance % (1000 * 60)) / 1000)

    container.value = {
      Hari: days,
      Jam: hours,
      Menit: minutes,
      Detik: seconds,
    }
  } else {
    container.value = {
      Hari: 0,
      Jam: 0,
      Menit: 0,
      Detik: 0,
    }
    onFinish()
  }
}

// Tanggal target: 9 September 2025 pukul 08:30 WIB
const targetDate = new Date('2025-09-09T08:30:00+07:00').getTime()

onMounted(() => {
  // Mulai countdown
  timer = setInterval(() => {
    createTimer(targetDate, countdown, () => {
      finished.value = true
      clearInterval(timer)
    })
  }, 1000)
})

onUnmounted(() => {
  // Bersihkan timer saat komponen dilepas
  if (timer) clearInterval(timer)
})
</script>

<style scoped>
/* Optional: kamu bisa tambahkan styling di sini jika perlu */
</style>