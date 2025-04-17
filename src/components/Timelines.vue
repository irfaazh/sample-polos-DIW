<style scoped>
.btn {
  @apply active:scale-95 active:ring-gray-200 active:ring duration-300 rounded-3xl px-3 py-2 text-amber-700 bg-orange-100 inline-block w-10/12 mt-4;
}
</style>

<template>
  <section class="w-full bg-gradient-to-b from-orange-50 to-orange-100">
    <section class="container-section pb-12">
      <HeaderSection text-color="text-amber-800" subtitle="Dengan tidak mengurangi rasa hormat, kami mengajak para tamu undangan agar bisa berhadir pada serangkaian acara kami" title="Runtutan Acara"></HeaderSection>
      <Card>
        <template v-slot:body>
          <div class="bg-amber-800 px-6 py-8 text-center text-sm font-medium" v-for="(timeline, index) in timelines" :key="index">
            <section data-aos="fade-up">
              <h1 class="text-xl satisfy-font text-amber-300">{{ timeline.title }}</h1>
              <p class="font-medium text-orange-50">{{ timeline.date }} | {{ timeline.time }}</p>
              <decoration class="w-2/12 mx-auto my-2 fill-amber-300"></decoration>
              <p class="text-orange-50">{{ timeline.location }}</p>
              <p class="text-orange-50">{{ timeline.address }}</p>
              <a class="btn" href="">
                <i class="fa-solid fa-map"></i>
                Lihat Peta
              </a>
              <decoration class="w-2/12 mx-auto my-2 fill-orange-50 rotate-180"></decoration>
            </section>
          </div>
        </template>
        <template v-slot:footer>
          <section class="bg-amber-800">
            <Countdown></Countdown>
            <!-- Button to Guest Book -->
            <div class="px-6 pt-5 pb-8 text-center">
              <p class="text-sm text-orange-50">Konfirmasi kehadiran anda pada buku tamu</p>
              <button @click="goToGuestBook" class="btn">
                <i class="fa-solid fa-clipboard-check"></i>
                Konfirmasi
              </button>
            </div>
           
          </section>
        </template>
      </Card>
    </section>
  </section>
</template>

<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'
import HeaderSection from '@/components/HeaderSection.vue'
import Card from '@/components/Card.vue'
import Countdown from '@/components/Countdown.vue'
// import decoration from '@/assets/svg/decoration-2.svg'

const timelines = ref(null)
onMounted(() => {
  axios.get('contents/timelines.json')
    .then( res => timelines.value = res.data.timelines )
    .catch( err => alert(err) )
})

// Handler for navigate to guest book
const emits = defineEmits(['goToGuestBook'])

const goToGuestBook = () => setTimeout(() => { emits('goToGuestBook') }, 300)
</script>