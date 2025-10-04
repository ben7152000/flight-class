<template>
  <section ref="elementRef" id="faq" class="faq-section" :class="{ 'fade-in-up': isVisible }">
    <div v-if="isVisible" class="container">
      <h2 class="section-title">常見問題</h2>

      <div class="faq-grid">
        <div
          v-for="(faq, index) in faqs"
          :key="index"
          class="faq-card"
          :class="{ active: activeIndex === index }"
          @click="toggleFAQ(index)"
        >
          <div class="faq-header">
            <div class="faq-number">{{ String(index + 1).padStart(2, '0') }}</div>
            <h3 class="faq-question">{{ faq.question }}</h3>
            <div class="faq-icon" :class="{ rotated: activeIndex === index }">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="6 9 12 15 18 9"></polyline>
              </svg>
            </div>
          </div>
          <transition name="expand">
            <div v-if="activeIndex === index" class="faq-answer">
              <p>{{ faq.answer }}</p>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'

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

const activeIndex = ref(null)

const faqs = ref([
  {
    question: '一架飛機可以乘載多少人？',
    answer: '除了機師以外只能搭乘一名乘客。',
  },
  {
    question: '有哪些時段可以飛行？',
    answer: 'AM 05:20 - PM 17:00，你可以自行選擇飛行的時間，若有特殊需求可以洽詢客服人員。',
  },
  {
    question: '我能在飛行中拍照嗎？',
    answer:
      '可以的，盡情在捕捉難得的烏瞰畫面，來一張空中機艙內帥氣的自拍照吧！特別注意請避免使用自拍棍，會影響教官操作飛行上的安全。',
  },
  {
    question: '夥伴不參加，是否可以在飛行場觀看？',
    answer: '可以在跑道旁觀看帥氣的起降過程，同時也可以側拍一照片，或者至休息室等候課程結束。',
  },
  {
    question: '我不希望有太刺激的飛行操作可以嗎？',
    answer: '沒問題的，只要事先和教官說明，也可以單純享受一般飛行觀光的體驗。',
  },
])

const toggleFAQ = (index) => {
  activeIndex.value = activeIndex.value === index ? null : index
}
</script>

<style lang="scss" scoped>
@use '../styles/variables.scss' as *;
@use '../styles/mixins.scss' as *;

.faq-section {
  @include section;
  background: $gradient-light;
  @include fade-in-section;
}

.faq-section.fade-in-up {
  opacity: 1;
  transform: translateY(0);
}

.container {
  @include container-md;
}

.section-title {
  @include section-title;
  font-weight: 700;
  text-align: center;
  display: inline-block;
  width: auto;
  position: relative;
}

.faq-grid {
  display: grid;
  gap: 1.5rem;
}

.faq-card {
  @include card;
  cursor: pointer;
  border: 2px solid transparent;

  &.active {
    border-color: $primary-dark;
    background: $gradient-blue;
  }
}

.faq-header {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.faq-number {
  flex-shrink: 0;
  width: 48px;
  height: 48px;
  background: $gradient-primary;
  color: $bg-white;
  border-radius: $border-radius-md;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: $font-size-lg;
  font-weight: 700;
  box-shadow: 0 4px 12px rgba(26, 108, 122, 0.3);
}

.faq-question {
  flex: 1;
  font-size: $font-size-lg;
  font-weight: 600;
  color: $secondary-color;
  margin: 0;
  line-height: 1.4;
}

.faq-icon {
  flex-shrink: 0;
  color: $primary-dark;
  transition: transform $transition-smooth;

  &.rotated {
    transform: rotate(180deg);
  }
}

.faq-answer {
  margin-top: 1.5rem;
  padding-top: 1.5rem;
  border-top: 2px solid rgba(26, 108, 122, 0.1);

  p {
    font-size: $font-size-sm;
    color: $text-medium;
    line-height: 1.8;
    margin: 0;
  }
}

.expand-enter-active,
.expand-leave-active {
  transition: all $transition-smooth;
  overflow: hidden;
}

.expand-enter-from,
.expand-leave-to {
  opacity: 0;
  max-height: 0;
  margin-top: 0;
  padding-top: 0;
}

.expand-enter-to,
.expand-leave-from {
  opacity: 1;
  max-height: 500px;
}

@media (max-width: 768px) {
  .container {
    padding: $container-padding-mobile;
  }

  .section-title {
    font-size: $font-size-2xl;
    margin-bottom: 2.5rem;
  }

  .faq-card {
    padding: 1.5rem;
  }

  .faq-header {
    gap: 1rem;
  }

  .faq-number {
    width: 40px;
    height: 40px;
    font-size: $font-size-sm;
  }

  .faq-question {
    font-size: $font-size-sm;
  }

  .faq-answer p {
    font-size: $font-size-xs;
  }
}
</style>
