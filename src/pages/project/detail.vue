<template>
  <view class="project-detail-container">
    <view class="placeholder-content">
      <text class="placeholder-icon">📊</text>
      <text class="placeholder-title">项目详情</text>
      <text class="placeholder-desc">此功能正在开发中...</text>
    </view>
  </view>
</template>

<script setup>
import { onLoad } from '@dcloudio/uni-app'

onLoad((options) => {
  if (options.type) {
    console.log('项目类型:', options.type)
  }
})
</script>

<style lang="scss" scoped>
.project-detail-container {
  min-height: 100vh;
  background: #f5f7fa;
  display: flex;
  align-items: center;
  justify-content: center;
}

.placeholder-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20rpx;
}

.placeholder-icon {
  font-size: 120rpx;
}

.placeholder-title {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
}

.placeholder-desc {
  font-size: 28rpx;
  color: #999;
}
</style>

