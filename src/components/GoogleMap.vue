<template>
  <div class="google-map">
    <div class="map-container">
      <iframe
        :src="mapSrc"
        :width="width"
        :height="height"
        style="border: 0"
        allowfullscreen=""
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  // Google Maps 嵌入網址或地點名稱
  location: {
    type: String,
    required: true,
  },
  // 地圖寬度
  width: {
    type: String,
    default: '100%',
  },
  // 地圖高度
  height: {
    type: String,
    default: '450',
  },
  // 縮放等級
  zoom: {
    type: Number,
    default: 15,
  },
})

const mapSrc = computed(() => {
  // 如果是 Google Maps 短網址 (maps.app.goo.gl)，轉換為可嵌入的格式
  if (props.location.includes('maps.app.goo.gl') || props.location.includes('goo.gl')) {
    // 將短網址轉換為普通連結格式，讓用戶點擊開啟
    return props.location.replace('maps.app.goo.gl', 'www.google.com/maps/d')
  }

  // 如果是完整的 Google Maps 嵌入網址，直接使用
  if (props.location.startsWith('http')) {
    return props.location
  }

  // 否則使用地點名稱生成 Google Maps 嵌入網址
  const encodedLocation = encodeURIComponent(props.location)
  return `https://www.google.com/maps?q=${encodedLocation}&output=embed&z=${props.zoom}`
})
</script>

<style scoped>
.google-map {
  width: 100%;
}

.map-container {
  position: relative;
  width: 100%;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.map-container iframe {
  display: block;
  width: 100%;
}

/* Responsive */
@media (max-width: 768px) {
  .map-container {
    border-radius: 5px;
  }
}
</style>
