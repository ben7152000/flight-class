<script setup>
import { ref } from 'vue'
import Carousel from './components/Carousel.vue'

// Carousel data
const carouselSlides = ref([
  {
    image: 'https://images.unsplash.com/photo-1559827260-dc66d52bef19?w=1200&h=600&fit=crop',
    title: '探索海洋世界',
    description: '專業潛水教學，開啟您的水下冒險'
  },
  {
    image: 'https://images.unsplash.com/photo-1544551763-46a013bb70d5?w=1200&h=600&fit=crop',
    title: 'PADI 國際認證',
    description: '取得全球認可的潛水證照'
  },
  {
    image: 'https://images.unsplash.com/photo-1682687220742-aba13b6e50ba?w=1200&h=600&fit=crop',
    title: '龍洞潛水基地',
    description: '台北最佳潛水訓練場地'
  }
])
</script>

<template>
  <div class="diving-page">
    <!-- Image Carousel -->
    <Carousel :slides="carouselSlides" :autoplayInterval="5000" />

    <!-- Hero Section -->
    <section class="hero">
      <div class="container">
        <h1>台北學潛水｜水肺潛水證照課程體驗報名</h1>
        <p class="subtitle">推薦評價團隊 - Long Dong 龍洞潛水基地</p>
        <button class="cta-button">立即報名</button>
      </div>
    </section>

    <!-- Course Content Section -->
    <section id="course" class="course-section">
      <div class="container">
        <h2 class="section-title">3. 課程項目內容</h2>

        <div class="course-grid">
          <div class="course-card">
            <div class="course-icon">🌊</div>
            <h3>PADI 開放水域潛水員課程</h3>
            <p>取得國際認證的水肺潛水證照，開啟您的水下探險之旅。課程包含理論學習、平靜水域訓練及開放水域潛水實習。</p>
            <ul class="course-features">
              <li>✓ 5 堂理論課程</li>
              <li>✓ 5 次平靜水域訓練</li>
              <li>✓ 4 次開放水域潛水</li>
              <li>✓ 國際認證證照</li>
            </ul>
          </div>

          <div class="course-card">
            <div class="course-icon">🤿</div>
            <h3>進階開放水域潛水員</h3>
            <p>提升您的潛水技能，探索更多水下活動。包含深潛、導航及三項專長潛水訓練。</p>
            <ul class="course-features">
              <li>✓ 5 次開放水域潛水</li>
              <li>✓ 深潛訓練</li>
              <li>✓ 水下導航</li>
              <li>✓ 專長項目選擇</li>
            </ul>
          </div>

          <div class="course-card">
            <div class="course-icon">🏊</div>
            <h3>體驗潛水</h3>
            <p>無需證照，即可體驗水肺潛水的樂趣。專業教練全程陪同，適合初次嘗試潛水的朋友。</p>
            <ul class="course-features">
              <li>✓ 安全簡報</li>
              <li>✓ 基礎技巧教學</li>
              <li>✓ 專業教練陪同</li>
              <li>✓ 裝備提供</li>
            </ul>
          </div>

          <div class="course-card">
            <div class="course-icon">⚓</div>
            <h3>救援潛水員課程</h3>
            <p>學習如何預防及處理潛水緊急狀況，成為更安全、更負責任的潛水員。</p>
            <ul class="course-features">
              <li>✓ 自救技巧</li>
              <li>✓ 救援技巧</li>
              <li>✓ 緊急應變</li>
              <li>✓ CPR 訓練</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about-section">
      <div class="container">
        <h2 class="section-title">為什麼選擇我們？</h2>
        <div class="about-grid">
          <div class="about-item">
            <h3>專業教練團隊</h3>
            <p>所有教練皆持有 PADI 專業證照，經驗豐富，熱愛潛水教學。</p>
          </div>
          <div class="about-item">
            <h3>優質訓練場地</h3>
            <p>位於台北近郊的龍洞，擁有清澈的海水和豐富的海洋生態。</p>
          </div>
          <div class="about-item">
            <h3>小班制教學</h3>
            <p>採用小班制教學，確保每位學員都能獲得充分的指導與練習。</p>
          </div>
          <div class="about-item">
            <h3>完善裝備</h3>
            <p>提供高品質的潛水裝備，定期保養維護，確保安全無虞。</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact-section">
      <div class="container">
        <h2 class="section-title">聯絡我們</h2>
        <div class="contact-info">
          <div class="contact-item">
            <h3>📍 地址</h3>
            <p>台北市龍洞潛水基地</p>
          </div>
          <div class="contact-item">
            <h3>📞 電話</h3>
            <p>02-XXXX-XXXX</p>
          </div>
          <div class="contact-item">
            <h3>✉️ Email</h3>
            <p>info@taipeidiving.com</p>
          </div>
          <div class="contact-item">
            <h3>🕐 營業時間</h3>
            <p>週一至週日 9:00-18:00</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  line-height: 1.6;
  color: #333;
}

/* Color Scheme */
:root {
  --primary-color: #1a6c7a;
  --secondary-color: #153243;
  --light-bg: #f3f9fb;
  --white: #ffffff;
  --text-dark: #333333;
  --text-light: #666666;
}

/* Container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Hero Section */
.hero {
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
  color: var(--white);
  padding: 6rem 0;
  text-align: center;
}

.hero h1 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.subtitle {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  opacity: 0.9;
}

.cta-button {
  background: var(--white);
  color: var(--primary-color);
  border: none;
  padding: 1rem 3rem;
  font-size: 1.1rem;
  font-weight: bold;
  border-radius: 50px;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
}

.cta-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

/* Course Section */
.course-section {
  padding: 5rem 0;
  background: var(--white);
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  color: var(--secondary-color);
  margin-bottom: 3rem;
}

.course-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.course-card {
  background: var(--light-bg);
  padding: 2rem;
  border-radius: 15px;
  transition: transform 0.3s, box-shadow 0.3s;
}

.course-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 35px rgba(26, 108, 122, 0.2);
}

.course-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.course-card h3 {
  color: var(--primary-color);
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.course-card p {
  color: var(--text-light);
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.course-features {
  list-style: none;
}

.course-features li {
  padding: 0.5rem 0;
  color: var(--text-dark);
}

/* About Section */
.about-section {
  padding: 5rem 0;
  background: var(--light-bg);
}

.about-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.about-item {
  background: var(--white);
  padding: 2rem;
  border-radius: 10px;
  border-left: 4px solid var(--primary-color);
}

.about-item h3 {
  color: var(--secondary-color);
  margin-bottom: 1rem;
}

.about-item p {
  color: var(--text-light);
  line-height: 1.6;
}

/* Contact Section */
.contact-section {
  padding: 5rem 0;
  background: var(--white);
}

.contact-info {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 3rem;
}

.contact-item {
  text-align: center;
  padding: 2rem;
  background: var(--light-bg);
  border-radius: 10px;
}

.contact-item h3 {
  color: var(--primary-color);
  margin-bottom: 1rem;
  font-size: 1.3rem;
}

.contact-item p {
  color: var(--text-dark);
}

.social-links {
  display: flex;
  justify-content: center;
  gap: 2rem;
}

.social-link {
  padding: 1rem 2rem;
  background: var(--primary-color);
  color: var(--white);
  text-decoration: none;
  border-radius: 50px;
  transition: background 0.3s;
}

.social-link:hover {
  background: var(--secondary-color);
}

/* Footer */
.footer {
  background: var(--secondary-color);
  color: var(--white);
  text-align: center;
  padding: 2rem 0;
}

/* Responsive */
@media (max-width: 768px) {
  .hero h1 {
    font-size: 2rem;
  }

  .section-title {
    font-size: 2rem;
  }

  .course-grid,
  .about-grid,
  .contact-info {
    grid-template-columns: 1fr;
  }
}
</style>
