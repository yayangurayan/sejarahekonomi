<script setup>
import { ref } from 'vue'
import { historyData } from '@/data/history.js'
import EconomistCard from '@/components/EconomistCard.vue'
import { useWindowScroll } from '@vueuse/core'

const { y } = useWindowScroll()

// Helper untuk scroll halus ke era tertentu (opsional untuk navigasi masa depan)
const scrollToEra = (id) => {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <div class="min-h-screen bg-[#f9f3e0] font-sans overflow-x-hidden">
    
    <!-- Hero Section -->
    <header class="relative h-[50vh] min-h-[400px] flex flex-col justify-center items-center text-center px-4 overflow-hidden bg-gradient-to-b from-history-gold/10 to-[#f9f3e0]">
      <!-- Background Ornament -->
      <div class="absolute inset-0 opacity-5 pointer-events-none">
        <svg class="w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
          <path d="M0 100 C 20 0 50 0 100 100 Z" fill="currentColor" class="text-history-gold"/>
        </svg>
      </div>
      
      <div 
        class="relative z-10 max-w-4xl"
        :style="{ transform: `translateY(${y * 0.2}px)` }"
      >
        <div class="inline-block mb-4 px-4 py-1 rounded-full border border-history-gold/30 bg-white/50 backdrop-blur-sm text-history-gold text-xs font-bold tracking-[0.2em] uppercase">
          Ensiklopedia Ekonomi
        </div>
        <h1 class="text-4xl md:text-6xl lg:text-7xl font-extrabold mb-6 text-gray-800 tracking-tight">
          Sejarah Pemikiran <span class="text-transparent bg-clip-text bg-gradient-to-r from-history-gold to-amber-700">Ekonomi</span>
        </h1>
        <p class="text-lg md:text-xl text-gray-600 leading-relaxed max-w-2xl mx-auto">
          Jelajahi evolusi gagasan dari masa Yunani Kuno hingga era Digital. Sebuah perjalanan memahami bagaimana dunia bekerja.
        </p>
      </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4 pb-32 max-w-7xl">
      
      <!-- Timeline Connector Line -->
      <div class="hidden lg:block absolute left-1/2 top-[50vh] bottom-0 w-px bg-gradient-to-b from-history-gold/50 via-history-gold/20 to-transparent transform -translate-x-1/2 -z-10"></div>

      <!-- Loop Through Eras -->
      <section 
        v-for="(era, index) in historyData" 
        :key="index" 
        :id="'era-' + index"
        class="mb-32 relative scroll-mt-24"
      >
        <!-- Era Header -->
        <div class="flex flex-col items-center mb-12 relative z-10">
          <div class="sticky top-6 z-20 shadow-xl shadow-history-gold/10 rounded-full">
            <h2 class="bg-history-gold text-white px-8 py-2 rounded-full text-lg md:text-xl font-bold tracking-wide uppercase border-4 border-[#f9f3e0]">
              {{ era.era }}
            </h2>
          </div>
          <div class="mt-6 max-w-2xl text-center bg-white/60 backdrop-blur-sm p-4 rounded-xl border border-white/50 shadow-sm">
            <p class="text-gray-600 italic">"{{ era.description }}"</p>
          </div>
        </div>

        <!-- Cards Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6 lg:gap-8 px-2">
          <EconomistCard 
            v-for="(figure, fIndex) in era.figures" 
            :key="fIndex" 
            :figure="figure"
          />
        </div>
      </section>

      <!-- Footer Simple -->
      <footer class="text-center pt-12 border-t border-history-gold/20">
        <p class="text-history-gold font-semibold text-sm tracking-widest uppercase">Sejarah Pemikiran Ekonomi</p>
        <p class="text-gray-400 text-xs mt-2">Dibuat dengan Vue 3 & Tailwind CSS</p>
      </footer>

    </main>

    <!-- Quick Nav (Floating Bottom) -->
    <div class="fixed bottom-6 right-6 z-50 flex flex-col gap-2">
      <button 
        @click="window.scrollTo({ top: 0, behavior: 'smooth' })"
        class="p-3 bg-history-gold text-white rounded-full shadow-lg hover:bg-amber-600 transition-colors focus:outline-none"
        v-if="y > 500"
      >
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18"></path></svg>
      </button>
    </div>

  </div>
</template>