<template>
  <view class="custom-tabbar">
    <view 
      class="tab-item" 
      :class="{ active: current === 0 }"
      @click="switchTab(0, '/pages/index/index')"
    >
      <image 
        class="tab-icon" 
        :src="current === 0 ? '/static/tabbar/home-active.png' : '/static/tabbar/home.png'"
        mode="aspectFit"
      />
      <text class="tab-text">首页</text>
    </view>
    <view 
      class="tab-item" 
      :class="{ active: current === 1 }"
      @click="switchTab(1, '/pages/me/index')"
    >
      <image 
        class="tab-icon" 
        :src="current === 1 ? '/static/tabbar/me-active.png' : '/static/tabbar/me.png'"
        mode="aspectFit"
      />
      <text class="tab-text">我的</text>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const current = ref(0)

onMounted(() => {
  const pages = getCurrentPages()
  const currentPage = pages[pages.length - 1]
  const route = currentPage.route
  
  if (route === 'pages/index/index') {
    current.value = 0
  } else if (route === 'pages/me/index') {
    current.value = 1
  }
})

const switchTab = (index, url) => {
  if (current.value === index) return // 如果已经是当前页，不执行跳转
  current.value = index
  uni.switchTab({
    url: url,
    fail: (err) => {
      console.log('switchTab失败，使用reLaunch:', err)
      // 如果switchTab失败，使用reLaunch
      uni.reLaunch({ url })
    }
  })
}
</script>

<style lang="scss" scoped>
.custom-tabbar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100rpx;
  background: #ffffff;
  display: flex;
  align-items: center;
  justify-content: space-around;
  border-top: 1rpx solid #e5e7eb;
  box-shadow: 0 -2rpx 10rpx rgba(0, 0, 0, 0.05);
  z-index: 999;
  padding-bottom: env(safe-area-inset-bottom);
}

.tab-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 10rpx 0;
  transition: all 0.3s;
}

.tab-item:active {
  opacity: 0.7;
}

.tab-icon {
  width: 44rpx;
  height: 44rpx;
  margin-bottom: 4rpx;
}

.tab-text {
  font-size: 22rpx;
  color: #94a3b8;
  transition: color 0.3s;
}

.tab-item.active .tab-text {
  color: #1f8df2;
  font-weight: 600;
}
</style>

