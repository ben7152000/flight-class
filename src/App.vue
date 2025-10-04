<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import CryptoJS from 'crypto-js'
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
const encryptionKey = 'flight-class'

const getTokenFromURL = () => {
  const params = new URLSearchParams(window.location.search)
  return params.get('token')
}

const decryptToken = (encryptedToken) => {
  try {
    const bytes = CryptoJS.AES.decrypt(encryptedToken, encryptionKey)
    return bytes.toString(CryptoJS.enc.Utf8)
  } catch (error) {
    console.error('解密失敗:', error)
    return null
  }
}

const connectWebSocket = () => {
  ws = new WebSocket(url)

  ws.onopen = () => {
    const encryptedToken = getTokenFromURL()
    if (!encryptedToken) {
      window.location.href = forceUrl
      return
    }

    const token = decryptToken(encryptedToken)
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

// 防止右鍵選單
const disableContextMenu = (e) => {
  e.preventDefault()
  return false
}

// 防止複製、剪下
const disableCopyPaste = (e) => {
  e.preventDefault()
  return false
}

// 防止選取文字
const disableSelect = (e) => {
  e.preventDefault()
  return false
}

// 防止鍵盤快捷鍵（F12, Ctrl+Shift+I, Ctrl+Shift+C, Ctrl+U）
const disableDevTools = (e) => {
  // F12
  if (e.keyCode === 123) {
    e.preventDefault()
    return false
  }
  // Ctrl+Shift+I, Ctrl+Shift+C, Ctrl+Shift+J
  if (e.ctrlKey && e.shiftKey && (e.keyCode === 73 || e.keyCode === 67 || e.keyCode === 74)) {
    e.preventDefault()
    return false
  }
  // Ctrl+U (查看原始碼)
  if (e.ctrlKey && e.keyCode === 85) {
    e.preventDefault()
    return false
  }
  // Cmd+Option+I, Cmd+Option+C, Cmd+Option+J (Mac)
  if (e.metaKey && e.altKey && (e.keyCode === 73 || e.keyCode === 67 || e.keyCode === 74)) {
    e.preventDefault()
    return false
  }
}

onMounted(() => {
  connectWebSocket()

  // 添加事件監聽
  document.addEventListener('contextmenu', disableContextMenu)
  document.addEventListener('copy', disableCopyPaste)
  document.addEventListener('cut', disableCopyPaste)
  document.addEventListener('selectstart', disableSelect)
  document.addEventListener('keydown', disableDevTools)
})

onUnmounted(() => {
  if (pingInterval) {
    clearInterval(pingInterval)
  }
  if (ws) {
    ws.close()
  }

  // 移除事件監聽
  document.removeEventListener('contextmenu', disableContextMenu)
  document.removeEventListener('copy', disableCopyPaste)
  document.removeEventListener('cut', disableCopyPaste)
  document.removeEventListener('selectstart', disableSelect)
  document.removeEventListener('keydown', disableDevTools)
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
  <div v-else class="loading-container"></div>
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
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
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
  background-color: transparent;
}
</style>
