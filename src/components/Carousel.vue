<template>
  <section id="hero" class="hero">
    <div class="hero-container">
      <div class="hero-content">
        <h1 class="hero-title">
          全台灣最適合飛行的地點 - <span class="highlight">花蓮</span>
        </h1>
        <p class="hero-description">
          無論是觀光的體驗飛行，或者邁向機師夢的專業考照課程，都能在此一覽台灣神秘的花東仙境，擁抱縱谷鬼斧神工的天然美景。
        </p>
      </div>
      <div class="hero-image-wrapper">
        <img
          :src="hero1Image"
          alt="Flying"
          class="hero-image"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import hero1Image from '../assets/hero1.jpg'
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  background: #fafafa;
  padding: 0;
}

.hero-container {
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 60px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6rem;
  align-items: center;
}

.hero-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 1.2;
  color: #000;
}

.highlight {
  background: #ffe8d6;
  padding: 0 0.5rem;
  font-style: italic;
}

.hero-description {
  font-size: 1.1rem;
  color: #666;
  line-height: 1.6;
}

.cta-button {
  background: #9fd3c1;
  color: #000;
  padding: 1rem 2rem;
  border-radius: 8px;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 600;
  align-self: flex-start;
  transition: transform 0.3s, box-shadow 0.3s;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

.cta-button::after {
  content: '→';
  font-size: 1.2rem;
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(159, 211, 193, 0.4);
}

.hero-image-wrapper {
  position: relative;
  width: 100%;
  background: #ffe8d6;
  border-radius: 50%;
  overflow: hidden;
  aspect-ratio: 1/1;
}

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 768px) {
  .hero-container {
    grid-template-columns: 1fr;
    padding: 0 20px;
    gap: 2rem;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-description {
    font-size: 1rem;
  }
}
</style>
