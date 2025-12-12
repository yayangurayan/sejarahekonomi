<script setup>
import { ref } from 'vue'
import { historyData } from '@/data/history.js'
import EconomistCard from '@/components/EconomistCard.vue'
import { useWindowScroll } from '@vueuse/core'

const { y } = useWindowScroll()
</script>

<template>
  <div class="min-h-screen bg-[#f9f3e0] font-sans overflow-x-hidden">
    
    <!-- Hero Section -->
    <header class="relative h-[60vh] min-h-[500px] flex flex-col justify-center items-center text-center px-4 overflow-hidden bg-gradient-to-b from-history-gold/10 to-[#f9f3e0]">
      <!-- Background Ornament -->
      <div class="absolute inset-0 opacity-10 pointer-events-none">
        <svg class="w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
          <pattern id="grid" width="10" height="10" patternUnits="userSpaceOnUse">
            <path d="M 10 0 L 0 0 0 10" fill="none" stroke="currentColor" stroke-width="0.5"/>
          </pattern>
          <rect width="100" height="100" fill="url(#grid)" class="text-history-gold"/>
        </svg>
      </div>
      
      <div 
        class="relative z-10 max-w-4xl transition-transform duration-75 ease-out"
        :style="{ transform: `translateY(${y * 0.2}px)` }"
      >
        <div class="inline-block mb-6 px-4 py-1 rounded-full border border-history-gold/30 bg-white/50 backdrop-blur-sm text-history-gold text-xs font-bold tracking-[0.2em] uppercase shadow-sm">
          Ensiklopedia Ekonomi Digital
        </div>
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 text-gray-800 tracking-tight leading-tight">
          Sejarah Pemikiran <br>
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-history-gold to-yellow-700">Ekonomi</span>
        </h1>
        <p class="text-lg md:text-xl text-gray-600 leading-relaxed max-w-2xl mx-auto">
          Menelusuri jejak gagasan ekonomi dari masa klasik hingga era modern. Memahami masa lalu untuk merancang masa depan.
        </p>
      </div>

      <!-- Scroll Down Indicator -->
      <div class="absolute bottom-10 animate-bounce text-history-gold/70">
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path></svg>
      </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4 pb-32 max-w-7xl relative z-20">
      
      <!-- Timeline Vertical Line (Desktop Only) -->
      <div class="hidden lg:block absolute left-1/2 top-0 bottom-0 w-1 bg-gradient-to-b from-history-gold/50 via-history-gold/20 to-transparent transform -translate-x-1/2 -z-10 rounded-full"></div>

      <!-- Era Loop -->
      <section 
        v-for="(era, index) in historyData" 
        :key="index" 
        class="mb-32 relative scroll-mt-24"
      >
        <!-- Era Header Sticky -->
        <div class="flex flex-col items-center mb-16 sticky top-4 z-30">
          <div class="shadow-xl shadow-history-gold/20 rounded-full">
            <h2 class="bg-history-gold text-white px-8 py-3 rounded-full text-lg md:text-xl font-bold tracking-wide uppercase border-4 border-[#f9f3e0] shadow-sm">
              {{ era.era }}
            </h2>
          </div>
          <div class="mt-4 max-w-2xl text-center bg-white/80 backdrop-blur-md p-4 rounded-xl border border-white/50 shadow-sm transform translate-y-2">
            <p class="text-gray-600 italic font-medium">"{{ era.description }}"</p>
          </div>
        </div>

        <!-- Cards Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8 px-4">
          <EconomistCard 
            v-for="(figure, fIndex) in era.figures" 
            :key="fIndex" 
            :figure="figure"
            class="h-full"
          />
        </div>
      </section>

      <!-- Footer -->
      <footer class="text-center pt-12 border-t border-history-gold/20 mt-20">
        <p class="text-history-gold font-semibold text-sm tracking-widest uppercase">Sejarah Pemikiran Ekonomi</p>
        <p class="text-gray-400 text-xs mt-2">Dibuat dengan sentuhan Dewa wkwkwk</p>
      </footer>

    </main>

    <!-- Back to Top Button -->
    <div class="fixed bottom-8 right-8 z-50 transition-opacity duration-300" :class="{ 'opacity-0 pointer-events-none': y < 500, 'opacity-100': y >= 500 }">
      <button 
        @click="window.scrollTo({ top: 0, behavior: 'smooth' })"
        class="p-4 bg-history-gold text-white rounded-full shadow-xl hover:bg-yellow-600 transition-colors focus:outline-none hover:scale-110 transform duration-200"
      >
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18"></path></svg>
      </button>
    </div>

  </div>
</template>