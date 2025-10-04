<template>
  <section ref="elementRef" id="gallery" class="gallery-section" :class="{ 'fade-in-up': isVisible }">
    <div v-if="isVisible" class="container">
      <h2 class="section-title">相片集</h2>

      <div class="gallery-container">
        <div class="main-image-wrapper">
          <transition name="slide-fade" mode="out-in">
            <img :key="selectedIndex" :src="images[selectedIndex].url" :alt="images[selectedIndex].alt" class="main-image" />
          </transition>
        </div>

        <div class="thumbnail-grid">
          <div
            v-for="(image, index) in images"
            :key="index"
            class="thumbnail-item"
            :class="{ active: index === selectedIndex }"
            @click="selectImage(index)"
          >
            <img :src="image.url" :alt="image.alt" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
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

const selectedIndex = ref(0)

const selectImage = (index) => {
  selectedIndex.value = index
}

import img1 from '../assets/gallery/1.webp'
import img2 from '../assets/gallery/2.webp'
import img3 from '../assets/gallery/3.webp'
import img4 from '../assets/gallery/4.webp'
import img5 from '../assets/gallery/5.webp'
import img6 from '../assets/gallery/6.webp'

const images = ref([
  {
    url: img1,
    alt: '飛行訓練',
  },
  {
    url: img2,
    alt: '輕航機',
  },
  {
    url: img3,
    alt: '駕駛艙',
  },
  {
    url: img4,
    alt: '飛行體驗',
  },
  {
    url: img5,
    alt: '花東縱谷',
  },
  {
    url: img6,
    alt: '日出飛行',
  }
])
</script>

<style lang="scss" scoped>
@use '../styles/variables.scss' as *;
@use '../styles/mixins.scss' as *;

.gallery-section {
  @include section;
  background: $bg-white;
  @include fade-in-section;
}

.gallery-section.fade-in-up {
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

.gallery-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.main-image-wrapper {
  width: 100%;
  height: 700px;
  border-radius: $border-radius-lg;
  overflow: hidden;
  box-shadow: $shadow-lg;
  background: #000;
  position: relative;

  .main-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}

.slide-fade-enter-active {
  transition: all $transition-normal;
}

.slide-fade-leave-active {
  transition: all $transition-fast;
}

.slide-fade-enter-from {
  transform: scale(0.8) translateY(20px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: scale(0.95);
  opacity: 0;
}

.thumbnail-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 1rem;
}

.thumbnail-item {
  aspect-ratio: 4/3;
  border-radius: $border-radius-sm;
  overflow: hidden;
  cursor: pointer;
  position: relative;
  transition: all $transition-smooth;
  box-shadow: $shadow-sm;

  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    transition: opacity $transition-smooth;
    z-index: 1;
  }

  &.active::before {
    opacity: 0;
  }

  &.active {
    transform: scale(1.05);
    box-shadow: 0 4px 16px rgba(26, 108, 122, 0.4);
    border: 3px solid $primary-dark;
  }

  &:hover:not(.active) {
    transform: scale(1.03);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);

    &::before {
      opacity: 0.3;
    }
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
}

@media (max-width: 1024px) {
  .thumbnail-grid {
    grid-template-columns: repeat(4, 1fr);
  }

  .main-image-wrapper {
    height: 400px;
  }
}

@media (max-width: 768px) {
  .container {
    padding: $container-padding-mobile;
  }

  .section-title {
    font-size: $font-size-2xl;
  }

  .thumbnail-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 0.75rem;
  }

  .main-image-wrapper {
    height: 300px;
  }
}
</style>
