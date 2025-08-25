<template>
  <div class="absolute bottom-8 right-8 z-30">
    <div class="relative w-20 h-20 flex items-center justify-center">
      <!-- Pulsing Border Circle -->
      <PulsingBorder
        :colors="['#BEECFF', '#E77EDC', '#FF4C3E', '#00FF88', '#FFD700', '#FF6B35', '#8A2BE2']"
        color-back="#00000000"
        :speed="1.5"
        :roundness="1"
        :thickness="0.1"
        :softness="0.2"
        :intensity="5"
        :spots-per-color="5"
        :spot-size="0.1"
        :pulse="0.1"
        :smoke="0.5"
        :smoke-size="4"
        :scale="0.65"
        :rotation="0"
        :frame="9161408.251009725"
        :style="{
          width: '60px',
          height: '60px',
          borderRadius: '50%',
        }"
      />

      <!-- Rotating Text Around the Pulsing Border -->
      <svg
        class="absolute inset-0 w-full h-full"
        viewBox="0 0 100 100"
        :style="{ transform: `scale(1.6) rotate(${rotation}deg)` }"
      >
        <defs>
          <path id="circle" d="M 50, 50 m -38, 0 a 38,38 0 1,1 76,0 a 38,38 0 1,1 -76,0" />
        </defs>
        <text class="text-sm fill-white/80 instrument">
          <textPath href="#circle" startOffset="0%">
            v0 is amazing • v0 is amazing • v0 is amazing • v0 is amazing •
          </textPath>
        </text>
      </svg>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { PulsingBorder } from '@paper-design/shaders-react'

const rotation = ref(0)
let animationId = null

const animate = () => {
  rotation.value += 0.3
  animationId = requestAnimationFrame(animate)
}

onMounted(() => {
  animate()
})

onUnmounted(() => {
  if (animationId) {
    cancelAnimationFrame(animationId)
  }
})
</script>
