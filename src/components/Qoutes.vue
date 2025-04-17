<template>
    <div class="min-h-screen flex items-center justify-center bg-gradient-to-b from-gray-100 to-gray-100 p-4 md:p-8">
      <div class="relative max-w-2xl w-full bg-white rounded-xl shadow-lg overflow-hidden border border-amber-200">
        <!-- Decorative elements -->
        <div class="absolute -top-8 -left-8 w-16 h-16 bg-amber-50 rounded-full"></div>
        <div class="absolute -bottom-8 -right-8 w-16 h-16 bg-amber-50 rounded-full"></div>
        
        <!-- Logo section -->
         <div class="flex justify-center mt-8">
            <img src="/public/icons/icon-72x72.png" alt="Logo Islamic" class="w-20 h-20 object-cover rounded-full shadow-md">
        </div>
        
        <!-- Content -->
        <div class="p-6 md:p-8 text-center">
          <!-- Surah info -->
          <h2 class="text-amber-600 text-lg md:text-xl font-semibold mb-4">
            Surah Az Zariyat Ayat 49
          </h2>
          
          <!-- Arabic text -->
          <div class="text-2xl md:text-3xl leading-loose text-gray-800 font-arabic mb-6">
            وَمِنْ كُلِّ شَيْءٍ خَلَقْنَا زَوْجَيْنِ لَعَلَّكُمْ تَذَكَّرُوْنَ
          </div>
          
          <!-- Translation -->
          <div class="pt-4 border-t border-dashed border-amber-200">
            <p class="text-gray-600 italic">
              "Dan segala sesuatu Kami ciptakan berpasang-pasangan agar kamu mengingat (kebesaran Allah)."
            </p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'QuranQuote',
    // Anda bisa menambahkan props atau data jika diperlukan
  }
  </script>
  
  <style>
  /* Import font Arabic jika diperlukan */
  @import url('https://fonts.googleapis.com/css2?family=Amiri&display=swap');
  
  .font-arabic {
    font-family: 'Amiri', serif;
  }
  </style>