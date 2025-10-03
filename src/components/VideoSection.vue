<template>
  <section id="video" class="video-section">
    <div class="container">
      <h2 class="section-title">精彩影片</h2>
      <div class="video-wrapper">
        <iframe
          src="https://www.youtube.com/embed/IhA3yaUP3Ho"
          title="YouTube video player"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
          allowfullscreen
        ></iframe>
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

.video-section {
  padding: 5rem 0;
  background: $light-bg;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
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

.video-wrapper {
  position: relative;
  padding-bottom: 56.25%; // 16:9 aspect ratio
  height: 0;
  overflow: hidden;
  margin: 0 auto;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);

  iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 15px;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }

  .video-section {
    padding: 3rem 0;
  }
}
</style>
