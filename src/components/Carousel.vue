<template>
  <section class="carousel">
    <div class="carousel-container">
      <div class="carousel-slides" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
        <div v-for="(slide, index) in slides" :key="index" class="carousel-slide">
          <img :src="slide.image" :alt="slide.title" class="carousel-image">
          <div class="carousel-overlay">
            <div class="carousel-content">
              <h2 class="carousel-title">{{ slide.title }}</h2>
              <p class="carousel-description">{{ slide.description }}</p>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Carousel data
const slides = ref([
  {
    image: 'https://images.unsplash.com/photo-1559827260-dc66d52bef19?w=1200&h=600&fit=crop',
    title: '探索天空世界',
    description: '專業飛行教學，開啟您的空中冒險'
  },
  {
    image: 'https://images.unsplash.com/photo-1544551763-46a013bb70d5?w=1200&h=600&fit=crop',
    title: 'FAA 國際認證',
    description: '取得全球認可的飛行證照'
  },
  {
    image: 'https://images.unsplash.com/photo-1682687220742-aba13b6e50ba?w=1200&h=600&fit=crop',
    title: '專業飛行基地',
    description: '台灣最佳飛行訓練場地'
  }
])

const autoplayInterval = 5000
const currentSlide = ref(0)
let autoplayTimer = null

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.value.length
}

onMounted(() => {
  if (autoplayInterval > 0) {
    autoplayTimer = setInterval(nextSlide, autoplayInterval)
  }
})

onUnmounted(() => {
  if (autoplayTimer) {
    clearInterval(autoplayTimer)
  }
})
</script>

<style scoped>
/* Carousel Styles */
.carousel {
  position: relative;
  width: 100%;
  height: 600px;
  overflow: hidden;
}

.carousel-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.carousel-slides {
  display: flex;
  height: 100%;
  transition: transform 0.5s ease-in-out;
}

.carousel-slide {
  min-width: 100%;
  height: 100%;
  position: relative;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.5));
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel-content {
  text-align: center;
  color: white;
  padding: 2rem;
}

.carousel-title {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.carousel-description {
  font-size: 1.5rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

/* Responsive */
@media (max-width: 768px) {
  .carousel {
    height: 400px;
  }

  .carousel-title {
    font-size: 2rem;
  }

  .carousel-description {
    font-size: 1rem;
  }
}
</style>
