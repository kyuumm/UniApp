<template>
  <view class="custom-tabbar">
    <view 
      class="tab-item" 
      :class="{ active: current === 0 }"
      @click="switchTab(0, '/pages/index/index')"
    >
      <image 
        class="tab-icon" 
        :key="`home-${current}`"
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
        :key="`me-${current}`"
        :src="current === 1 ? '/static/tabbar/me-active.png' : '/static/tabbar/me.png'"
        mode="aspectFit"
      />
      <text class="tab-text">我的</text>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue'

const current = ref(0)

const updateCurrent = () => {
  try {
    const pages = getCurrentPages()
    if (pages && pages.length > 0) {
      const currentPage = pages[pages.length - 1]
      const route = currentPage?.route || ''
      
      if (route === 'pages/index/index') {
        current.value = 0
      } else if (route === 'pages/me/index') {
        current.value = 1
      }
    }
  } catch (e) {
    console.log('updateCurrent error:', e)
  }
}

onMounted(() => {
  updateCurrent()
  // 监听页面变化事件
  uni.$on('updateTabBar', (index) => {
    if (typeof index === 'number') {
      current.value = index
    } else {
      updateCurrent()
    }
  })
})

const switchTab = (index, url) => {
  if (current.value === index) return // 如果已经是当前页，不执行跳转
  
  // 立即更新状态，确保UI立即响应
  current.value = index
  
  // 使用nextTick确保状态更新后再执行跳转
  nextTick(() => {
    uni.switchTab({
      url: url,
      success: () => {
        // 切换成功后再次确认状态
        nextTick(() => {
          updateCurrent()
        })
      },
      fail: (err) => {
        console.log('switchTab失败，使用reLaunch:', err)
        uni.reLaunch({ 
          url,
          success: () => {
            nextTick(() => {
              updateCurrent()
            })
          }
        })
      }
    })
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

