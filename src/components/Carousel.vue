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

      <!-- Navigation Arrows -->
      <button class="carousel-btn carousel-btn-prev" @click="prevSlide">
        <span>‹</span>
      </button>
      <button class="carousel-btn carousel-btn-next" @click="nextSlide">
        <span>›</span>
      </button>

      <!-- Dots Indicator -->
      <div class="carousel-dots">
        <button
          v-for="(slide, index) in slides"
          :key="index"
          class="carousel-dot"
          :class="{ active: currentSlide === index }"
          @click="goToSlide(index)"
        ></button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  slides: {
    type: Array,
    required: true
  },
  autoplayInterval: {
    type: Number,
    default: 5000
  }
})

const currentSlide = ref(0)
let autoplayTimer = null

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % props.slides.length
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + props.slides.length) % props.slides.length
}

const goToSlide = (index) => {
  currentSlide.value = index
}

onMounted(() => {
  if (props.autoplayInterval > 0) {
    autoplayTimer = setInterval(nextSlide, props.autoplayInterval)
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

/* Carousel Navigation Buttons */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.3);
  border: none;
  color: white;
  font-size: 3rem;
  padding: 1rem 1.5rem;
  cursor: pointer;
  transition: background 0.3s;
  z-index: 10;
}

.carousel-btn:hover {
  background: rgba(255, 255, 255, 0.5);
}

.carousel-btn-prev {
  left: 2rem;
}

.carousel-btn-next {
  right: 2rem;
}

.carousel-btn span {
  line-height: 1;
}

/* Carousel Dots */
.carousel-dots {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 1rem;
  z-index: 10;
}

.carousel-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: background 0.3s;
}

.carousel-dot.active {
  background: white;
}

.carousel-dot:hover {
  background: rgba(255, 255, 255, 0.8);
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

  .carousel-btn {
    font-size: 2rem;
    padding: 0.5rem 1rem;
  }

  .carousel-btn-prev {
    left: 1rem;
  }

  .carousel-btn-next {
    right: 1rem;
  }
}
</style>
