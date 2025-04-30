<template>
  <section>
    <MainCover id="mainCover"></MainCover>
    <Qoutes id="quotes"></Qoutes>
    <GroomBride></GroomBride>
    <Timelines v-on:goToGuestBook="navigationHandler('#guest-book')"></Timelines>
    <!-- <OurGallery></OurGallery> -->
     <OurStory></OurStory>
    <Envelope id="envelope"></Envelope>
    <GuestBook id="guest-book"></GuestBook>
    <End id="end"></End>
  </section>
</template>

<script setup>
import MainCover from '@/components/MainCover.vue'
import GroomBride from '@/components/GroomBride.vue'
import Timelines from '@/components/Timelines.vue'
import OurGallery from '@/components/OurGallery.vue'
import Envelope from '@/components/Envelope.vue'
import GuestBook from '@/components/GuestBook.vue'
import End from '@/components/End.vue'
import Qoutes from '@/components/Qoutes.vue'
import OurStory from '@/components/OurStory.vue'

// Navigation handler
const navigationHandler = id => {
  document.querySelector(id).scrollIntoView({
    behavior: 'smooth'
  })
}

</script>
