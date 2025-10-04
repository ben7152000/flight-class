<template>
  <section ref="elementRef" id="courses" class="course-intro" :class="{ 'fade-in-up': isVisible }">
    <div v-if="isVisible" class="container">
      <h2 class="section-title">重點指引</h2>

      <div class="content-grid">
        <div class="image-section">
          <img :src="hero2Image" alt="飛行訓練" class="hero-image" />
        </div>

        <div class="info-cards">
          <div class="info-card requirements-card">
            <h3 class="card-title">參加條件</h3>
            <ul class="card-list">
              <li><span class="bullet">•</span>無須任何經驗</li>
              <li><span class="bullet">•</span>體重限制100公斤內</li>
              <li><span class="bullet">•</span>男女不拘，15歲以上</li>
              <li><span class="bullet">•</span>有近視也可以參加 (須配戴眼鏡)</li>
              <li><span class="bullet">•</span>中 / 英文教學，語言無障礙</li>
              <li><span class="bullet warning">⚠</span>心臟病、高血壓、懼高症、氣喘、癲癇、孕婦不可參加</li>
            </ul>
          </div>

          <div class="info-card includes-card">
            <h3 class="card-title">內容包含</h3>
            <ul class="card-list">
              <li><span class="bullet check">✓</span>專業機師教練全程陪同指導</li>
              <li><span class="bullet check">✓</span>最高級LSA輕航機，輕航機界法拉利</li>
              <li><span class="bullet check">✓</span>Glass Cockpit 電子觸碰螢幕</li>
              <li><span class="bullet check">✓</span>航空業界高級BOSS降噪耳機</li>
              <li><span class="bullet check">✓</span>俯瞰花東縱谷鬼斧神工的天然仙境</li>
            </ul>
          </div>
        </div>
      </div>

      <div class="info-card notice-card full-width">
        <h3 class="card-title">特別須知</h3>
        <p class="notice-text">
          團隊所屬LSA低翼輕航機有2架，可以支援2人同時起飛飛行，若想3人以上同時飛行，會使用高翼輕航機機型支援，或採輪飛方式執行，採輪飛方式的夥伴需特別注意後續時間排程。
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import hero2Image from '../assets/hero2.jpg'

const elementRef = ref(null)
const isVisible = ref(false)

useIntersectionObserver(
  elementRef,
  ([{ isIntersecting }]) => {
    if (isIntersecting) {
      isVisible.value = true
    }
  },
  { threshold: 0.1, rootMargin: '50px' }
)
</script>

<style lang="scss" scoped>
@import '../styles/variables.scss';
@import '../styles/mixins.scss';

.course-intro {
  @include section;
  background: $bg-light;
  @include fade-in-section;
}

.course-intro.fade-in-up {
  opacity: 1;
  transform: translateY(0);
}

.container {
  @include container;
}

.section-title {
  @include section-title;
  display: inline-block;
  width: auto;
  position: relative;
}

.content-grid {
  @include grid-2-col;
  align-items: center;
  margin-bottom: 2rem;
}

.image-section {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;

  .hero-image {
    width: 100%;
    height: auto;
    border-radius: $border-radius-xl;
    box-shadow: $shadow-xl;
    transition: transform $transition-fast;

    &:hover {
      transform: scale(1.02);
    }
  }

  .image-caption {
    margin-top: 1.5rem;
    padding: 1.5rem;
    background: $gradient-primary;
    border-radius: $border-radius-md;
    color: $bg-white;

    h3 {
      font-size: $font-size-lg;
      font-weight: 700;
      margin-bottom: 0.5rem;
    }

    p {
      font-size: $font-size-sm;
      opacity: 0.9;
      margin: 0;
    }
  }
}

.info-cards {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.info-card {
  background: $bg-white;
  border-radius: $border-radius-md;
  padding: 1.5rem;
  box-shadow: $shadow-md;
  transition: transform $transition-fast, box-shadow $transition-fast;
  border-left: 4px solid $primary-dark;

  &:hover {
    transform: translateX(8px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  }

  .card-icon {
    font-size: $font-size-xl;
    margin-bottom: 0.75rem;
  }

  .card-title {
    font-size: $font-size-lg;
    font-weight: 700;
    color: $secondary-color;
    margin-bottom: 1rem;
  }

  .card-list {
    list-style: none;
    padding: 0;
    margin: 0;

    li {
      padding: 0.4rem 0;
      font-size: $font-size-xs;
      color: $text-dark;
      line-height: 1.5;
      display: flex;
      align-items: flex-start;
      gap: 0.6rem;

      .bullet {
        flex-shrink: 0;
        font-weight: 700;
        color: $primary-color;
        margin-top: 0.1rem;

        &.check {
          color: #4caf50;
        }

        &.warning {
          color: $warning-color;
        }
      }
    }
  }

  .notice-text {
    font-size: $font-size-xs;
    color: $text-medium;
    line-height: 1.7;
    margin: 0;
  }
}

.requirements-card {
  border-left-color: $primary-color;
}

.includes-card {
  border-left-color: #4caf50;
}

.notice-card {
  border-left-color: $warning-color;
  background: linear-gradient(135deg, #fff9f5, $bg-white);

  &.full-width {
    width: 100%;

    .notice-text {
      max-width: 100%;
    }
  }
}

@media (max-width: 1024px) {
  .content-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
    margin-bottom: 2rem;
  }

  .image-section {
    order: -1;
  }
}

@media (max-width: 768px) {
  .container {
    padding: $container-padding-mobile;
  }

  .section-title {
    font-size: $font-size-2xl;
    margin-bottom: 2.5rem;
  }

  .info-card {
    padding: 1.5rem;

    .card-title {
      font-size: $font-size-lg;
    }

    .card-list li {
      font-size: $font-size-xs;
    }

    .notice-text {
      font-size: $font-size-xs;
    }
  }

  .image-caption {
    h3 {
      font-size: $font-size-md;
    }

    p {
      font-size: 0.9rem;
    }
  }
}
</style>
