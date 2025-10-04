<template>
  <section ref="elementRef" id="about" class="about-section" :class="{ 'fade-in-up': isVisible }">
    <div v-if="isVisible" class="container">
      <div class="content-block">
        <h2 class="section-label">關於花蓮</h2>
        <p class="content-text">
          花蓮是台灣完美的後花園，湛藍的太平洋、太魯閣、七星潭、花東縱谷、賞鯨、慕谷慕魚、錐麓古道等，深藏眾多奇麗秘境，而且為全台空氣品質優良的區域，不必擔心霧霾的災害影響，讓每一次飛行都能擁有最佳的能見度！
        </p>
      </div>

      <div class="content-block">
        <h2 class="section-label">飛行過程</h2>
        <p class="content-text">
          你可以順其自然的迎接教官駕駛般的操作，感受小飛機特有的機動性和離心力，或在地面課程時先與教官溝通，表示需要單純舒適平緩的觀光飛行即可。
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
const { isVisible, elementRef } = useLazyLoad()
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

.about-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 6rem 0;
  background: #fff;
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.about-section.fade-in-up {
  opacity: 1;
  transform: translateY(0);
}

.container {
  width: 100%;
}

.content-block {
  margin-bottom: 4rem;

  &:last-child {
    margin-bottom: 0;
  }
}

.section-label {
  font-size: 1.5rem;
  font-weight: 700;
  color: #ff6b35;
  margin-bottom: 1rem;
  border-left: 4px solid #ff6b35;
  padding-left: 1rem;
}

.content-text {
  font-size: 1.1rem;
  color: #333;
  line-height: 1.8;
  padding-left: 1.25rem;
}

@media (max-width: 768px) {
  .section-label {
    font-size: 1.3rem;
  }

  .content-text {
    font-size: 1rem;
  }
}
</style>
