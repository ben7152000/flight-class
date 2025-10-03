<template>
  <section id="introduction" class="course-section">
    <div class="container">
      <h2 class="section-title">體驗介紹</h2>
      <div class="introduction-content">
        <p>
          探索天空世界，從這裡開始。我們提供專業的飛行訓練課程，由經驗豐富的 FAA
          認證教練指導，讓您安全、有趣地學習飛行技能。
        </p>
      </div>
    </div>
  </section>
</template>

<script setup></script>

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

.course-section {
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

.introduction-content {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
  font-size: 1.2rem;
  color: $text-dark;
  line-height: 1.8;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }
}
</style>
