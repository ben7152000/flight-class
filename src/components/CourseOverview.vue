<template>
  <section ref="elementRef" id="intro" class="course-intro-section" :class="{ 'fade-in-up': isVisible }">
    <div v-if="isVisible" class="container">
      <h2 class="section-title">課程簡介</h2>
      <div class="intro-image-wrapper">
        <img :src="infoImage" alt="課程簡介" class="intro-image" />
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import infoImage from '../assets/info.webp'

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
</script>

<style lang="scss" scoped>
@use '../styles/variables.scss' as *;
@use '../styles/mixins.scss' as *;

.course-intro-section {
  @include section;
  background: $bg-white;
  @include fade-in-section;
}

.course-intro-section.fade-in-up {
  opacity: 1;
  transform: translateY(0);
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

.intro-image-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;

  .intro-image {
    width: 100%;
    max-width: 1200px;
    height: auto;
    border-radius: $border-radius-lg;
    box-shadow: $shadow-lg;
  }
}

@media (max-width: 768px) {
  .container {
    padding: $container-padding-mobile;
  }

  .section-title {
    font-size: $font-size-2xl;
  }

  .intro-image-wrapper {
    .intro-image {
      border-radius: $border-radius-md;
    }
  }
}
</style>
