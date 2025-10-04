<template>
  <section
    ref="elementRef"
    id="map"
    class="map-section-wrapper"
    :class="{ 'slide-in': isVisible }"
  >
    <div v-if="isVisible" class="container">
      <h2 class="section-title">交通位置</h2>
      <div class="map-container">
        <GoogleMap :location="hualienLocation" height="700" :zoom="14" />
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import GoogleMap from './GoogleMap.vue'
import { useIntersectionObserver } from '@vueuse/core'

const elementRef = ref(null)
const isVisible = ref(false)

useIntersectionObserver(
  elementRef,
  ([{ isIntersecting }]) => {
    if (isIntersecting) {
      isVisible.value = true
    }
  },
  { threshold: 0.1, rootMargin: '50px' }
)

// Google Map location - 使用嵌入網址
const hualienLocation = ref(
  'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d18294.9057719069!2d121.48994475275818!3d23.812653181852998!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3468af6f21bad979%3A0x625830d2feeb9fca!2z6Iqx6JOu6LyV6Iiq5qmfLemdnuWHoemjm-ihjOWgtA!5e0!3m2!1szh-TW!2stw!4v1759478589440!5m2!1szh-TW!2stw'
)
</script>

<style lang="scss" scoped>
@use '../styles/variables.scss' as *;
@use '../styles/mixins.scss' as *;

.map-section-wrapper {
  @include section;
  background: $bg-white;
  opacity: 0;
  transform: translateX(-50px);
  transition: opacity $transition-slow, transform $transition-slow;
}

.map-section-wrapper.slide-in {
  opacity: 1;
  transform: translateX(0);
}

.container {
  @include container;
}

.section-title {
  @include section-title;
  text-align: center;
  display: inline-block;
  width: auto;
  position: relative;
}

.map-container {
  max-width: 1200px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .map-section-wrapper {
    padding: 2rem 0;
  }

  .container {
    padding: $container-padding-mobile;
  }

  .section-title {
    font-size: 1.5rem;
    margin-bottom: 1.5rem;
  }
}
</style>
