<template>
  <ShaderBackground>
   <Header />
    <HeroContent />
    <PulsingCircle />
  </ShaderBackground>
  <animated-background />
</template>

<script setup>

import HeroContent from './components/HeroContent.vue'
import PulsingCircle from './components/PulsingCircle.vue'
import ShaderBackground from './components/ShaderBackground.vue'
import AnimatedBackground from './components/AnimatedBackground.vue'
import Header from './components/Header.vue'
</script>
