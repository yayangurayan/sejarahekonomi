<script setup>
import { ref } from 'vue'
import { useElementVisibility } from '@vueuse/core'

const props = defineProps({
  figure: {
    type: Object,
    required: true
  }
})

const cardRef = ref(null)
const isVisible = useElementVisibility(cardRef)
const isExpanded = ref(false)

// Generate avatar dengan inisial dan warna dinamis
const getAvatarUrl = (name) => {
  const seed = name.length
  const colors = ['d99a5c', 'e6b47a', '8e6c4d', '555555', 'b8860b']
  const color = colors[seed % colors.length]
  return `https://ui-avatars.com/api/?name=${encodeURIComponent(name)}&background=${color}&color=fff&size=128&bold=true`
}

const toggleExpand = () => {
  isExpanded.value = !isExpanded.value
}
</script>

<template>
  <div 
    ref="cardRef"
    class="relative flex flex-col items-center bg-white rounded-xl shadow-lg transition-all duration-500 hover:shadow-2xl cursor-pointer group overflow-hidden border-t-4 border-history-gold"
    :class="{ 
      'opacity-0 translate-y-20': !isVisible, 
      'opacity-100 translate-y-0': isVisible,
      'ring-4 ring-history-gold/50 scale-[1.02] z-10': isExpanded,
      'hover:-translate-y-2': !isExpanded
    }"
    @click="toggleExpand"
  >
    <!-- Card Header Decoration -->
    <div class="absolute top-0 w-full h-24 bg-gradient-to-b from-history-cream to-white opacity-50 pointer-events-none"></div>

    <div class="p-6 flex flex-col items-center w-full relative z-10">
      <!-- Image with Ring Animation -->
      <div class="relative mb-4">
        <div class="absolute -inset-1 rounded-full bg-history-gold opacity-0 group-hover:opacity-100 group-hover:animate-ping transition duration-500"></div>
        <img 
          :src="getAvatarUrl(figure.name)" 
          :alt="figure.name" 
          class="relative w-24 h-24 rounded-full object-cover border-4 border-white shadow-md transition-transform duration-500 group-hover:scale-110 group-hover:rotate-3 bg-gray-200"
          loading="lazy"
        >
      </div>

      <!-- Badge -->
      <span class="mb-3 px-3 py-1 bg-history-gold/10 text-history-gold text-xs font-bold uppercase tracking-wider rounded-full border border-history-gold/20">
        {{ figure.title }}
      </span>

      <!-- Content -->
      <h3 class="text-xl font-bold text-gray-800 text-center leading-tight mb-1">{{ figure.name }}</h3>
      <p class="text-sm text-history-gold font-semibold mb-4">{{ figure.year }}</p>

      <!-- Expandable Description -->
      <div class="w-full relative bg-history-paper/50 rounded-lg p-2">
        <div 
          class="transition-all duration-500 ease-in-out overflow-hidden"
          :style="{ maxHeight: isExpanded ? '500px' : '60px' }"
        >
          <p class="text-gray-600 text-sm leading-relaxed text-center px-2">
            {{ figure.desc }}
          </p>
        </div>
        
        <!-- Fade effect for collapsed state -->
        <div 
          v-if="!isExpanded"
          class="absolute bottom-0 left-0 w-full h-12 bg-gradient-to-t from-white to-transparent pointer-events-none"
        ></div>
      </div>

      <!-- Indicator Icon -->
      <div class="mt-4 transition-transform duration-300" :class="{ 'rotate-180': isExpanded }">
        <svg class="w-6 h-6 text-history-gold" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
        </svg>
      </div>
    </div>
  </div>
</template>