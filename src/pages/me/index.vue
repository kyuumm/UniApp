<template>
  <view class="me-container">
    <!-- 用户信息头部 -->
    <view class="user-header">
      <view class="user-avatar">
        <text class="avatar-text">{{ userInfo.name ? userInfo.name.charAt(0) : 'U' }}</text>
      </view>
      <view class="user-info">
        <text class="user-name">{{ userInfo.name || '未登录' }}</text>
        <text class="user-role">{{ userInfo.role || '游客' }}</text>
      </view>
    </view>

    <!-- 功能列表 -->
    <view class="function-list">
      <!-- 我的下载/收藏 -->
      <view class="function-section">
        <view class="section-title">我的内容</view>
        <view class="function-item" @click="goToMyDownload">
          <view class="function-icon" style="background: linear-gradient(135deg, #88b0f6 0%, #4facfe 100%);">
            📥
          </view>
          <text class="function-text">我的下载</text>
          <text class="function-arrow">→</text>
        </view>
        <view class="function-item" @click="goToMyCollection">
          <view class="function-icon" style="background: linear-gradient(135deg, #fec47e 0%, #ff9a56 100%);">
            ⭐
          </view>
          <text class="function-text">我的收藏</text>
          <text class="function-arrow">→</text>
        </view>
      </view>

      <!-- 我的项目/报表 -->
      <view class="function-section">
        <view class="section-title">项目管理</view>
        <view class="function-item" @click="goToMyProject">
          <view class="function-icon" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
            📊
          </view>
          <text class="function-text">我的项目</text>
          <text class="function-arrow">→</text>
        </view>
        <view class="function-item" @click="goToMyReport">
          <view class="function-icon" style="background: linear-gradient(135deg, #daedbb 0%, #a8e063 100%);">
            📈
          </view>
          <text class="function-text">我的报表</text>
          <text class="function-arrow">→</text>
        </view>
      </view>

      <!-- 报销相关 -->
      <view class="function-section">
        <view class="section-title">财务报销</view>
        <view class="function-item" @click="goToExpense">
          <view class="function-icon" style="background: linear-gradient(135deg, #fec47e 0%, #ff9a56 100%);">
            💰
          </view>
          <text class="function-text">手机报销</text>
          <text class="function-arrow">→</text>
        </view>
        <view class="function-item" @click="goToInvoice">
          <view class="function-icon" style="background: linear-gradient(135deg, #88b0f6 0%, #4facfe 100%);">
            🧾
          </view>
          <text class="function-text">电子发票</text>
          <text class="function-arrow">→</text>
        </view>
        <view class="function-item" @click="goToExpenseAnalysis">
          <view class="function-icon" style="background: linear-gradient(135deg, #daedbb 0%, #a8e063 100%);">
            📊
          </view>
          <text class="function-text">报销分析</text>
          <text class="function-arrow">→</text>
        </view>
      </view>

      <!-- 管理员入口（根据权限显示） -->
      <view class="function-section" v-if="userInfo.role === 'admin'">
        <view class="section-title">管理员</view>
        <view class="function-item" @click="goToAdmin">
          <view class="function-icon" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);">
            ⚙️
          </view>
          <text class="function-text">管理后台</text>
          <text class="function-arrow">→</text>
        </view>
      </view>
    </view>

    <!-- 退出登录 -->
    <view class="logout-section">
      <button class="logout-btn" @click="handleLogout">退出登录</button>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

const userInfo = ref({
  name: '张三',
  role: 'student' // student / teacher / admin
})

// 跳转到我的下载
const goToMyDownload = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 跳转到我的收藏
const goToMyCollection = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 跳转到我的项目
const goToMyProject = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 跳转到我的报表
const goToMyReport = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 跳转到财务报销
const goToExpense = () => {
  uni.navigateTo({
    url: '/pages/expense/home'
  })
}

// 跳转到电子发票
const goToInvoice = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 跳转到报销分析
const goToExpenseAnalysis = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 跳转到管理后台
const goToAdmin = () => {
  uni.showToast({
    title: '功能开发中',
    icon: 'none'
  })
}

// 退出登录
const handleLogout = () => {
  uni.showModal({
    title: '提示',
    content: '确定要退出登录吗？',
    success: (res) => {
      if (res.confirm) {
        uni.reLaunch({
          url: '/pages/login/login'
        })
      }
    }
  })
}
</script>

<style lang="scss" scoped>
.me-container {
  min-height: 100vh;
  background: linear-gradient(180deg, #f5f7fa 0%, #ffffff 100%);
  padding-bottom: 40rpx;
}

// 用户信息头部
.user-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #4facfe 100%);
  padding: 60rpx 30rpx 40rpx;
  display: flex;
  align-items: center;
  gap: 30rpx;
}

.user-avatar {
  width: 120rpx;
  height: 120rpx;
  border-radius: 60rpx;
  background: rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
  display: flex;
  align-items: center;
  justify-content: center;
  border: 4rpx solid rgba(255, 255, 255, 0.5);
}

.avatar-text {
  font-size: 48rpx;
  font-weight: bold;
  color: #fff;
}

.user-info {
  display: flex;
  flex-direction: column;
  gap: 10rpx;
  flex: 1;
}

.user-name {
  font-size: 36rpx;
  font-weight: bold;
  color: #fff;
}

.user-role {
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.8);
  background: rgba(255, 255, 255, 0.2);
  padding: 4rpx 16rpx;
  border-radius: 12rpx;
  align-self: flex-start;
}

// 功能列表
.function-list {
  padding: 30rpx;
}

.function-section {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 24rpx;
  margin-bottom: 30rpx;
  overflow: hidden;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
}

.section-title {
  font-size: 28rpx;
  font-weight: 600;
  color: #666;
  padding: 30rpx 30rpx 20rpx;
  border-bottom: 1rpx solid #f0f0f0;
}

.function-item {
  display: flex;
  align-items: center;
  padding: 30rpx;
  border-bottom: 1rpx solid #f5f5f5;
  transition: all 0.3s;
}

.function-item:last-child {
  border-bottom: none;
}

.function-item:active {
  background: #f8f8f8;
}

.function-icon {
  width: 80rpx;
  height: 80rpx;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 40rpx;
  margin-right: 24rpx;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.1);
}

.function-text {
  flex: 1;
  font-size: 30rpx;
  color: #333;
}

.function-arrow {
  font-size: 28rpx;
  color: #ccc;
}

// 退出登录
.logout-section {
  padding: 0 30rpx;
  margin-top: 40rpx;
}

.logout-btn {
  width: 100%;
  height: 100rpx;
  background: #fff;
  border-radius: 50rpx;
  color: #ff6b6b;
  font-size: 32rpx;
  font-weight: 500;
  border: 2rpx solid #ff6b6b;
  display: flex;
  align-items: center;
  justify-content: center;
}

.logout-btn:active {
  background: #fff5f5;
}
</style>

