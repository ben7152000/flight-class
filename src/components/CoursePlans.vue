<template>
  <section id="plans" class="plans-section">
    <div class="container">
      <h2 class="section-title">體驗方案</h2>

      <div class="course-grid">
        <div class="course-card">
          <div class="course-icon">✈️</div>
          <h3>私人飛行員執照課程</h3>
          <p>取得國際認證的私人飛行員執照，開啟您的空中探險之旅。課程包含理論學習、模擬飛行訓練及實際飛行實習。</p>
          <ul class="course-features">
            <li>✓ 40 小時飛行訓練</li>
            <li>✓ 理論課程學習</li>
            <li>✓ 模擬器訓練</li>
            <li>✓ 國際認證執照</li>
          </ul>
        </div>

        <div class="course-card">
          <div class="course-icon">🛩️</div>
          <h3>商業飛行員執照</h3>
          <p>提升您的飛行技能，探索更多航空領域。包含儀表飛行、夜間飛行及專業飛行訓練。</p>
          <ul class="course-features">
            <li>✓ 250 小時飛行時數</li>
            <li>✓ 儀表飛行訓練</li>
            <li>✓ 夜間飛行</li>
            <li>✓ 專業認證</li>
          </ul>
        </div>

        <div class="course-card">
          <div class="course-icon">🪂</div>
          <h3>體驗飛行</h3>
          <p>無需執照，即可體驗飛行的樂趣。專業飛行員全程陪同，適合初次嘗試飛行的朋友。</p>
          <ul class="course-features">
            <li>✓ 安全簡報</li>
            <li>✓ 基礎操作教學</li>
            <li>✓ 專業飛行員陪同</li>
            <li>✓ 30 分鐘飛行體驗</li>
          </ul>
        </div>

        <div class="course-card">
          <div class="course-icon">🚁</div>
          <h3>直升機飛行課程</h3>
          <p>學習直升機飛行技術，掌握垂直起降與懸停技能，成為專業的直升機飛行員。</p>
          <ul class="course-features">
            <li>✓ 懸停訓練</li>
            <li>✓ 垂直起降</li>
            <li>✓ 緊急應變</li>
            <li>✓ 專業認證</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
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

.plans-section {
  padding: 5rem 0;
  background: $light-bg;
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

.course-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.course-card {
  background: $white;
  padding: 2rem;
  border-radius: 15px;
  transition: transform 0.3s, box-shadow 0.3s;

  &:hover {
    transform: translateY(-10px);
    box-shadow: 0 15px 35px rgba(26, 108, 122, 0.2);
  }

  h3 {
    color: $primary-color;
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }

  p {
    color: $text-light;
    margin-bottom: 1.5rem;
    line-height: 1.6;
  }
}

.course-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.course-features {
  list-style: none;

  li {
    padding: 0.5rem 0;
    color: $text-dark;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }

  .course-grid {
    grid-template-columns: 1fr;
  }
}
</style>
