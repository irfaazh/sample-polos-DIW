<template>
  <section class="w-full bg-gradient-to-b from-orange-50 to-orange-100 pt-12 pb-5">
    <section class="section-container">
      <HeaderSection title="Amplop Digital" subtitle=" Doa restu anda merupakan karunia yang sangat berarti bagi kami dan jika memberi adalah ungkapan tanda terima kasih anda, anda dapat memberi kado secara cashless"></HeaderSection>
      <section class="">

        <template v-for="(wallet, x) in wallets" :key="x">
          <div data-aos="zoom-in" class="w-8/12 text-center border border-orange-50 mx-auto p-5 mb-5 bg-orange-200 shadow-lg rounded-tl-3xl rounded-br-3xl">
            <img :src="wallet.thumb" :alt="wallet.platform" class="w-5/12 mx-auto mb-3">
            
            <!-- Card for bank transfers -->
            <template v-if="wallet.prefix">
              <p class="text-xs">Silahkan untuk melakukan transfer melalui {{ wallet.prefix }} dibawah ini a.n. {{ wallet.name }}</p>
              <Clipboard :content="wallet.number"></Clipboard>
            </template>
            
            <!-- Card for gift -->
            <template v-else>
              <p class="text-xs">Silahkan jika ingin mengirim kado penerima a.n</p>
              <p class="text-sm font-medium mt-2">{{ wallet.nama }}</p>
              <Clipboard :content="wallet.alamat"></Clipboard>
            </template>
          </div>
        </template>
      </section>
    </section>
  </section>
</template>

<script setup>
import HeaderSection from '@/components/HeaderSection.vue'
import Clipboard from '@/components/Clipboard.vue'

const wallets = [
  {
    thumb: 'wallets/bca.png',
    platform: 'bca',
    name: 'REVA HAMIDAH',
    number: 'xxxxx',
    prefix: 'rekening'
  },
  {
    thumb: 'wallets/bni.png',
    platform: 'BNI',
    name: 'MOCHAMMAD AKMAL ABDULLAH',
    number: 'xxxxxxx',
    prefix: 'rekening'
  },
  {
    thumb: 'wallets/gift.png',
    platform: 'gift',
    nama: 'Reva Hamidah',
    alamat: 'Perum Grand Appel Bojong Malaka Kec Pameungpeuk Kab Bandung',
    tujuan: 'sending gift'
  }
]
</script>