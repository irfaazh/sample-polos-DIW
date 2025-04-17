<template>
  <section class="w-full bg-gradient-to-b from-orange-100 to-orange-50">
    <section class="container-section">
      <HeaderSection text-color="text-amber-800" title="Kisah Cinta Kami" />
      
      <div class="mt-8 px-4">
        <!-- Stories Bubbles -->
        <div class="w-full max-w-3xl mx-auto">
          <template v-for="(story, x) in stories" :key="x">
            <!-- Chat Bubble Item -->
            <div data-aos="fade-up" class="mb-16 relative">
              <!-- Title Pill at top -->
              <div class="absolute -top-4 left-4 z-10 bg-amber-500 text-orange-50 text-sm font-semibold px-4 py-2 rounded-xl shadow-sm">
                {{ story.title }}
              </div>
              
              <!-- Content Bubble -->
              <div class="bg-amber-800 rounded-2xl p-6 pt-10 shadow-sm">
                <p v-if="story.place" class="font-medium mb-3 text-center text-orange-50">{{ story.place }}</p>
                <p class="text-orange-50 leading-relaxed text-justify text-sm">{{ story.description }}</p>
              </div>
            </div>
          </template>
        </div>
      </div>
    </section>
  </section>
</template>

<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'
import HeaderSection from '@/components/HeaderSection.vue'

const stories = ref(null)
onMounted(() => {
  axios.get('contents/story.json')
    .then(res => stories.value = res.data.stories)
    .catch(err => alert(err))
})
</script>

<style scoped>
.satisfy-font {
  font-family: 'Satisfy', cursive;
}
</style>