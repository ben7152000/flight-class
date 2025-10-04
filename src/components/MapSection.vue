<template>
  <section
    ref="elementRef"
    id="map"
    class="map-section-wrapper"
    :class="{ 'slide-in': isVisible }"
  >
    <div v-if="isVisible" class="container">
      <h2 class="section-title">交通位置</h2>
      <div class="map-grid">
        <div class="map-item">
          <h3>花蓮</h3>
          <GoogleMap :location="hualienLocation" height="350" :zoom="14" />
        </div>
        <div class="map-item">
          <h3>屏東</h3>
          <GoogleMap :location="pingtungLocation" height="350" :zoom="14" />
        </div>
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

// Google Map locations - 使用嵌入網址
const hualienLocation = ref(
  'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d18294.9057719069!2d121.48994475275818!3d23.812653181852998!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3468af6f21bad979%3A0x625830d2feeb9fca!2z6Iqx6JOu6LyV6Iiq5qmfLemdnuWHoemjm-ihjOWgtA!5e0!3m2!1szh-TW!2stw!4v1759478589440!5m2!1szh-TW!2stw'
)
const pingtungLocation = ref(
  'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2860.854261963873!2d120.62326306902018!3d22.754727498477205!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x346e3ed35f422479%3A0x522632806790b3c8!2z6LO95ZiJ55qG6LGq6LyV6Iiq5qmf6aOb6KGM5aC077yI6ZyA6aCQ57SE77yJ!5e0!3m2!1szh-TW!2stw!4v1759551201468!5m2!1szh-TW!2stw'
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

.map-grid {
  @include grid-2-col;
}

.map-item {
  h3 {
    color: $primary-dark;
    font-size: $font-size-xl;
    margin-bottom: 1.5rem;
    text-align: center;
  }
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

  .map-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .map-item h3 {
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }
}
</style>
