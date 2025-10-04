<template>
  <section ref="elementRef" id="pricing" class="pricing" :class="{ 'fade-in-up': isVisible }">
    <div v-if="isVisible" class="container">
      <h2 class="section-title">課程價格</h2>
      <div class="pricing-header">
        <p class="pricing-note">超夯課程，請盡量於一週前預約</p>
      </div>

      <div class="pricing-table">
        <div class="table-header">
          <div class="header-col">課程方案</div>
          <div class="header-col highlight">新推廣價 <span class="tag">特價</span></div>
          <div class="header-col">課程售價</div>
        </div>

        <template v-for="(plan, index) in plans.slice(0, 3)" :key="index">
          <div class="pricing-row">
            <div class="plan-name">
              <div>{{ plan.name }}</div>
              <div class="plan-subtitle">{{ plan.subtitle }}</div>
            </div>
            <div class="plan-price new-price">{{ plan.newPrice }}</div>
            <div class="plan-price old-price">{{ plan.oldPrice }}</div>
          </div>
        </template>

        <div class="table-header special">
          <div class="header-text">特殊方案</div>
        </div>

        <template v-for="(plan, index) in plans.slice(3)" :key="index + 3">
          <div class="pricing-row">
            <div class="plan-name">
              <div>{{ plan.name }}</div>
              <div class="plan-subtitle">{{ plan.subtitle }}</div>
            </div>
            <div class="plan-price new-price">{{ plan.newPrice }}</div>
            <div class="plan-price old-price">{{ plan.oldPrice || '' }}</div>
          </div>
        </template>

        <div class="note-section">所有項目一人即可報名</div>
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

const plans = ref([
  {
    name: '20分鐘飛行',
    subtitle: '10分鐘地面解說',
    newPrice: 'NT$ 5,000/人',
    oldPrice: 'NT$ 7,500/人',
  },
  {
    name: '30分鐘飛行',
    subtitle: '10分鐘地面解說',
    newPrice: 'NT$ 6,000/人',
    oldPrice: 'NT$ 8,500/人',
  },
  {
    name: '60分鐘飛行',
    subtitle: '15分鐘地面解說',
    newPrice: 'NT$ 12,000/人',
    oldPrice: 'NT$ 14,500/人',
  },
  {
    name: '日出曙光 (限花蓮)',
    subtitle: '60分鐘飛行',
    newPrice: 'NT$ 12,500/人',
    oldPrice: 'NT$ 15,000/人',
    isSpecial: true,
  },
  {
    name: '金針花海 (限花蓮)',
    subtitle: '60分鐘飛行',
    newPrice: 'NT$ 12,500/人',
    oldPrice: 'NT$ 15,000/人',
    isSpecial: true,
  },
  {
    name: '專業考照',
    subtitle: '操作證 / 教練證',
    newPrice: '請洽客服專員',
    isSpecial: true,
  },
])
</script>

<style lang="scss" scoped>
@import '../styles/variables.scss';
@import '../styles/mixins.scss';

.pricing {
  @include section;
  background: $bg-light;
  @include fade-in-section;
}

.pricing.fade-in-up {
  opacity: 1;
  transform: translateY(0);
}

.container {
  @include container-md;
}

.section-title {
  @include section-title;
  text-align: center;
  display: inline-block;
  width: auto;
  position: relative;
}

.pricing-header {
  text-align: center;
  margin-bottom: 2rem;
}

.pricing-note {
  font-size: $font-size-md;
  color: $text-dark;
  margin-bottom: 1.5rem;
}

.contact-btn {
  background: $accent-color;
  color: #000;
  padding: 0.75rem 2rem;
  border-radius: 50px;
  text-decoration: none;
  font-size: $font-size-sm;
  font-weight: 600;
  display: inline-block;
  transition: transform $transition-fast, box-shadow $transition-fast;
}

.contact-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(159, 211, 193, 0.4);
}

.pricing-table {
  background: $bg-white;
  border-radius: $border-radius-sm;
  overflow: hidden;
  box-shadow: $shadow-sm;
}

.table-header {
  background: #6ea8a3;
  color: $bg-white;
  display: grid;
  grid-template-columns: 2fr 1.5fr 1.5fr;
  padding: 1rem 2rem;
  font-weight: 600;

  &.special {
    grid-template-columns: 1fr;
    text-align: center;
    padding: 0.75rem;
  }
}

.header-col {
  &.highlight {
    background: #6ea8a3;
  }
}

.tag {
  background: #ffeb3b;
  color: #000;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  font-size: 0.8rem;
  margin-left: 0.5rem;
}

.pricing-row {
  display: grid;
  grid-template-columns: 2fr 1.5fr 1.5fr;
  padding: 1.5rem 2rem;
  border-bottom: 1px solid #e5e5e5;

  &:last-of-type {
    border-bottom: none;
  }
}

.plan-name {
  font-size: $font-size-sm;
  color: $text-dark;

  div:first-child {
    font-weight: 600;
  }
}

.plan-subtitle {
  font-size: 0.9rem;
  color: $text-light;
  margin-top: 0.25rem;
}

.plan-price {
  font-size: $font-size-sm;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;

  &.new-price {
    font-weight: 700;
    color: $text-dark;
  }

  &.old-price {
    color: $text-muted;
    text-decoration: line-through;
  }
}

.note-section {
  background: $bg-light;
  padding: 1rem;
  text-align: center;
  font-size: $font-size-xs;
  color: $text-light;
}

@media (max-width: 768px) {
  .container {
    padding: $container-padding-mobile;
  }

  .table-header,
  .pricing-row {
    grid-template-columns: 1fr;
    gap: 0.5rem;
    padding: 1rem;
  }

  .plan-price {
    justify-content: flex-start;
  }

  .pricing-note,
  .plan-name,
  .plan-price {
    font-size: 0.9rem;
  }
}
</style>
