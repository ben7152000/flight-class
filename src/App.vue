<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Navigation from './components/Navigation.vue'
import Carousel from './components/Carousel.vue'
import KeyHighlights from './components/KeyHighlights.vue'
import CourseOverview from './components/CourseOverview.vue'
import Gallery from './components/Gallery.vue'
import VideoSection from './components/VideoSection.vue'
import FAQ from './components/FAQ.vue'
import Pricing from './components/Pricing.vue'
import MapSection from './components/MapSection.vue'
import ScrollToTop from './components/ScrollToTop.vue'

let ws = null
let pingInterval = null
const isAuthorized = ref(false)

const url = 'wss://flight-class-server.ben7152000.workers.dev/ws'
const forceUrl = 'https://www.google.com'

const getTokenFromURL = () => {
  const params = new URLSearchParams(window.location.search)
  return params.get('token')
}

const connectWebSocket = () => {
  ws = new WebSocket(url)

  ws.onopen = () => {
    const token = getTokenFromURL()
    if (!token) {
      window.location.href = forceUrl
      return
    }

    ws.send(JSON.stringify({ type: 'enter', token }))

    pingInterval = setInterval(() => {
      if (ws && ws.readyState === WebSocket.OPEN) {
        ws.send(JSON.stringify({ type: 'ping' }))
      }
    }, 30000)
  }

  ws.onmessage = (event) => {
    try {
      const data = JSON.parse(event.data)
      if (data.type === 'pong') {
      } else if (data.type === 'success') {
        isAuthorized.value = true
      } else if (data.type === 'expired') {
        window.location.href = forceUrl
      } else if (data.type === 'error') {
        window.location.href = forceUrl
      }
    } catch (error) {
      console.error('解析訊息失敗:', error)
    }
  }

  ws.onerror = (error) => {
    console.error('WebSocket 錯誤:', error)
  }

  ws.onclose = () => {
    if (pingInterval) {
      clearInterval(pingInterval)
    }
  }
}

onMounted(() => {
  connectWebSocket()
})

onUnmounted(() => {
  if (pingInterval) {
    clearInterval(pingInterval)
  }
  if (ws) {
    ws.close()
  }
})
</script>

<template>
  <div v-if="isAuthorized" class="app-container">
    <Navigation />
    <main>
      <Carousel />
      <KeyHighlights />
      <CourseOverview />
      <Gallery />
      <VideoSection />
      <FAQ />
      <Pricing />
      <MapSection />
    </main>
    <ScrollToTop />
  </div>
  <div v-else class="loading-container">
    <div class="spinner"></div>
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  scroll-padding-top: 80px;
}

body {
  font-family:
    -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  line-height: 1.6;
  color: #333;
}

/* 隱藏滾動條但保持滾動功能 */
html::-webkit-scrollbar,
body::-webkit-scrollbar {
  display: none;
}

html,
body {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.app-container {
  position: relative;
  min-height: 100vh;
}

.loading-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}

.spinner {
  width: 60px;
  height: 60px;
  border: 4px solid rgba(92, 225, 184, 0.2);
  border-top-color: #5ce1b8;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}
</style>
