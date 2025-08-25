<template>
    <div ref="containerRef" class="min-h-screen bg-black relative overflow-hidden">

      <!-- SVG Filters -->
      <svg class="absolute inset-0 w-0 h-0">
        <defs>
          <filter id="glass-effect" x="-50%" y="-50%" width="200%" height="200%">
            <feTurbulence baseFrequency="0.005" numOctaves="1" result="noise" />
            <feDisplacementMap in="SourceGraphic" in2="noise" scale="0.3" />
            <feColorMatrix
              type="matrix"
              values="1 0 0 0 0.02
                      0 1 0 0 0.02
                      0 0 1 0 0.05
                      0 0 0 0.9 0"
              result="tint"
            />
          </filter>
          <filter id="gooey-filter" x="-50%" y="-50%" width="200%" height="200%">
            <feGaussianBlur in="SourceGraphic" stdDeviation="4" result="blur" />
            <feColorMatrix
              in="blur"
              mode="matrix"
              values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -9"
              result="gooey"
            />
            <feComposite in="SourceGraphic" in2="gooey" operator="atop" />
          </filter>
        </defs>
      </svg>
  
      <!-- Background Shaders -->
      <MeshGradient
        class="absolute inset-0 w-full h-full"
        :colors="['#000000', '#8b5cf6', '#ffffff', '#1e1b4b', '#4c1d95']"
        :speed="0.3"
        background-color="#000000"
      />
      <MeshGradient
        class="absolute inset-0 w-full h-full opacity-60"
        :colors="['#000000', '#ffffff', '#8b5cf6', '#000000']"
        :speed="0.2"
        wireframe="true"
        background-color="transparent"
      />
  
      <slot />
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted } from 'vue'
  import { MeshGradient } from '@paper-design/shaders-react'
  
  const containerRef = ref(null)
  const isActive = ref(false)
  
  const handleMouseEnter = () => {
    isActive.value = true
  }
  
  const handleMouseLeave = () => {
    isActive.value = false
  }
  
  onMounted(() => {
    const container = containerRef.value
    if (container) {
      container.addEventListener('mouseenter', handleMouseEnter)
      container.addEventListener('mouseleave', handleMouseLeave)
    }
  })
  
  onUnmounted(() => {
    const container = containerRef.value
    if (container) {
      container.removeEventListener('mouseenter', handleMouseEnter)
      container.removeEventListener('mouseleave', handleMouseLeave)
    }
  })
  </script>
  