<template>
  <section class="w-full bg-gradient-to-b from-orange-100 to-orange-50">
    <wave class="fill-white" />
    <section class="container-section">
      <!-- Arabic Calligraphy and Welcome Message -->
      <div class="text-center mb-8 px-4 invite-container">
        <div class="arabic-calligraphy mb-4 text-amber-800">بِسْمِ اللهِ الرَّحْمَنِ الرَّحِيمِ</div>
        <p class="text-amber-800 font-medium">Assalamu'alaikum Wr. Wb.</p>
        <p class="text-amber-800 mt-2">Tanpa mengurangi rasa hormat. Kami mengundang</p>
        <p class="text-amber-800">Bapak/Ibu/Saudara/i serta kerabat sekalian untuk menghadiri acara</p>
        <p class="text-amber-800">pernikahan kami:</p>
      </div>
      <HeaderSection text-color="text-amber-800" title="Mempelai Pria dan Wanita" subtitle="Ya Allah dengan mengharap ridha dan karunia-Mu, Izinkanlah kami mempersatukan dua insan dari dua keluarga ini agar menjadi pasangan yang selalu mendapakan rahmat-Mu" />
    
      <Profile></Profile>
    </section>
  </section>
</template>

<script setup>
import HeaderSection from '@/components/HeaderSection.vue'
import Profile from '@/components/Profile.vue'
import Timelines from '@/components/Timelines.vue'
import wave from '@/assets/svg/wave.svg'
</script>

<style scoped>
.arabic-calligraphy {
  font-family: 'Amiri', 'Scheherazade New', serif;
  font-size: 2rem;
  line-height: 1.8;
}

.invite-container {
  padding: 2rem 1rem;
  margin-bottom: 3rem;
}
</style>