<template>
  <section ref="elementRef" id="video" class="video-section" :class="{ 'slide-up': isVisible }">
    <div class="container">
      <h2 class="section-title">精彩影片</h2>
      <div v-if="isVisible" class="video-wrapper">
        <video autoplay loop muted playsinline>
          <source :src="pilotVideo" type="video/mp4" />
        </video>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import pilotVideo from '../assets/video/pilot-video.mp4'

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

.video-section {
  @include section;
  background: $bg-blue-light;
  @include fade-in-section;
}

.video-section.slide-up {
  opacity: 1;
  transform: translateY(0);
}

.container {
  @include container-md;
}

.section-title {
  @include section-title;
  text-align: center;
  display: inline-block;
  width: auto;
  position: relative;
}

.video-wrapper {
  position: relative;
  width: 100%;
  margin: 0 auto;
  border-radius: $border-radius-lg;
  overflow: hidden;
  box-shadow: $shadow-lg;

  video {
    width: 100%;
    height: auto;
    display: block;
    border-radius: $border-radius-lg;
  }
}

@media (max-width: 768px) {
  .video-section {
    display: none;
  }
}
</style>
