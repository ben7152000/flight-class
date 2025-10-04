<template>
  <nav class="navigation" :class="{ scrolled: isScrolled }">
    <div class="nav-container">
      <div class="logo">
        <span class="logo-text">Flight</span>
        <span class="logo-dot">.</span>
      </div>

      <button class="hamburger" :class="{ active: isMenuOpen }" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
      </button>

      <div class="overlay" :class="{ active: isMenuOpen }" @click="closeMenu"></div>

      <ul class="nav-menu" :class="{ active: isMenuOpen }">
        <li v-for="item in navItems" :key="item.id" :class="{ 'hide-on-mobile': item.hideOnMobile }">
          <a href="#" @click.prevent="scrollToSection(item.id)">{{ item.title }}</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const navItems = ref([
  { id: 'courses', title: '重點指引' },
  { id: 'intro', title: '課程簡介' },
  { id: 'gallery', title: '相片集' },
  { id: 'video', title: '精彩影片', hideOnMobile: true },
  { id: 'faq', title: '常見問題' },
  { id: 'pricing', title: '課程價格' },
  { id: 'map', title: '交通位置' },
])

const isMenuOpen = ref(false)
const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const scrollToSection = (sectionId) => {
  closeMenu()
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style lang="scss" scoped>
@use '../styles/variables.scss' as *;

.navigation {
  background: $bg-white;
  padding: 1.5rem 0;
  position: sticky;
  top: 0;
  z-index: 1000;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  transition: all $transition-fast;

  &.scrolled {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    padding: 1rem 0;
  }
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  font-size: 1.8rem;
  font-weight: 600;
  font-style: italic;
  z-index: 1001;

  .logo-text {
    color: $text-dark;
  }

  .logo-dot {
    color: $primary-color;
    font-size: 2rem;
  }
}

.hamburger {
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 0.4rem;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  z-index: 1001;
  width: 40px;
  height: 40px;
  position: relative;

  span {
    width: 25px;
    height: 3px;
    background: $text-dark;
    border-radius: 2px;
    transition: all $transition-fast;
    position: absolute;
  }

  span:nth-child(1) {
    top: 11px;
  }

  span:nth-child(2) {
    top: 18.5px;
  }

  span:nth-child(3) {
    top: 26px;
  }

  &.active {
    span:nth-child(1) {
      top: 18.5px;
      transform: rotate(45deg);
    }

    span:nth-child(2) {
      opacity: 0;
    }

    span:nth-child(3) {
      top: 18.5px;
      transform: rotate(-45deg);
    }
  }
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2.5rem;
  margin: 0;
  padding: 0;

  li {
    a {
      color: $text-dark;
      text-decoration: none;
      font-size: $font-size-sm;
      font-weight: 400;
      transition: opacity $transition-fast;

      &:hover {
        opacity: 0.7;
      }
    }
  }
}

@media (max-width: 1024px) {
  .hamburger {
    display: flex;
  }

  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    opacity: 0;
    visibility: hidden;
    transition: opacity $transition-smooth, visibility $transition-smooth;
    z-index: 998;

    &.active {
      opacity: 1;
      visibility: visible;
    }
  }

  .nav-menu {
    position: fixed;
    top: 0;
    right: -100%;
    width: 280px;
    height: 100vh;
    background: $bg-white;
    flex-direction: column;
    padding: 5rem 2rem 2rem;
    gap: 2rem;
    box-shadow: $shadow-xl;
    transition: right $transition-smooth;
    z-index: 999;

    &.active {
      right: 0;
    }

    li {
      a {
        font-size: $font-size-lg;
        display: block;
        padding: 0.5rem 0;
      }
    }
  }
}

@media (max-width: 768px) {
  .nav-container {
    padding: 0 20px;
  }

  .hide-on-mobile {
    display: none;
  }
}
</style>
