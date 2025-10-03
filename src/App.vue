<script setup>
import Carousel from './components/Carousel.vue'
import Navigation from './components/Navigation.vue'
import VideoSection from './components/VideoSection.vue'
import CourseIntroduction from './components/CourseIntroduction.vue'
import CoursePlans from './components/CoursePlans.vue'
import MapSection from './components/MapSection.vue'
</script>

<template>
  <div>
    <Carousel />
    <Navigation />
    <VideoSection />
    <CourseIntroduction />
    <CoursePlans />
    <MapSection />
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  line-height: 1.6;
  color: #333;
}
</style>
