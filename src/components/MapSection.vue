<template>
  <section id="map" class="map-section-wrapper">
    <div class="container">
      <h2 class="section-title">交通位置</h2>
      <div class="map-grid">
        <div class="map-item">
          <h3>花蓮位置</h3>
          <GoogleMap :location="hualienLocation" height="350" :zoom="14" />
        </div>
        <div class="map-item">
          <h3>屏東位置</h3>
          <GoogleMap :location="pingtungLocation" height="350" :zoom="14" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import GoogleMap from './GoogleMap.vue'

// Google Map locations - 使用嵌入網址
const hualienLocation = ref(
  'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d18294.9057719069!2d121.48994475275818!3d23.812653181852998!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3468af6f21bad979%3A0x625830d2feeb9fca!2z6Iqx6JOu6LyV6Iiq5qmfLemdnuWHoemjm-ihjOWgtA!5e0!3m2!1szh-TW!2stw!4v1759478589440!5m2!1szh-TW!2stw'
)
const pingtungLocation = ref(
  'https://www.google.com/maps/embed?pb=!1m10!1m8!1m3!1d1458.0696413459295!2d120.62196933547534!3d22.755318876699867!3m2!1i1024!2i768!4f13.1!5e0!3m2!1szh-TW!2stw!4v1759479752107!5m2!1szh-TW!2stw'
)
</script>

<style lang="scss" scoped>
// Color Variables
$primary-color: #1a6c7a;
$secondary-color: #153243;
$light-bg: #f3f9fb;
$white: #ffffff;
$text-dark: #333333;
$text-light: #666666;

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.map-section-wrapper {
  padding: 5rem 0;
  background: $white;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  color: $secondary-color;
  margin-bottom: 3rem;
  padding-bottom: 1rem;
  border-bottom: 3px solid $primary-color;
  display: inline-block;
  width: auto;
  position: relative;
}

.map-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 3rem;
}

.map-item {
  h3 {
    color: $primary-color;
    font-size: 1.5rem;
    margin-bottom: 1.5rem;
    text-align: center;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }
}
</style>
