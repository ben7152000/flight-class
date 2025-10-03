<template>
  <nav class="navigation">
    <div class="container">
      <ul class="nav-menu">
        <li v-for="item in navItems" :key="item.id">
          <a :href="`#${item.id}`">{{ item.title }}</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const navItems = ref([])

onMounted(() => {
  // 获取所有带有 id 的 section 元素
  const sections = document.querySelectorAll('section[id]')

  navItems.value = Array.from(sections).map(section => {
    const titleElement = section.querySelector('.section-title')
    return {
      id: section.id,
      title: titleElement ? titleElement.textContent : section.id
    }
  })
})
</script>

<style lang="scss" scoped>
// Color Variables
$primary-color: #1a6c7a;
$secondary-color: #153243;
$white: #ffffff;

.navigation {
  background: $secondary-color;
  color: $white;
  padding: 1rem 0;
  position: sticky;
  top: 0;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
  margin: 0;
  padding: 0;

  li {
    a {
      color: $white;
      text-decoration: none;
      font-size: 1.1rem;
      transition: color 0.3s;
      padding: 0.5rem 1rem;
      border-radius: 5px;

      &:hover {
        color: $white;
        background: rgba(255, 255, 255, 0.1);
      }
    }
  }
}

@media (max-width: 768px) {
  .container {
    flex-direction: column;
    gap: 1rem;
  }

  .nav-menu {
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
  }
}
</style>
