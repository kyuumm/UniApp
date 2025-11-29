<template>
  <view class="home-container">
    <!-- Logo区域 -->
    <view class="logo-section">
      <view class="logo-placeholder">
        <image class="logo-img" src="/static/logo.png" mode="aspectFit"></image>
      </view>
    </view>

    <!-- 快速入口 -->
    <view class="quick-entry-section">
      <view class="entry-card entry-left" @click="goToRepo">
        <view class="entry-icon" style="background: linear-gradient(135deg, #88b0f6 0%, #4facfe 100%);">
          📚
        </view>
        <text class="entry-text">资料下载</text>
      </view>
      <view class="entry-card entry-right" @click="goToExpense">
        <view class="entry-icon" style="background: linear-gradient(135deg, #fec47e 0%, #ff9a56 100%);">
          💰
        </view>
        <text class="entry-text">财务报销</text>
      </view>
    </view>

    <!-- 案例分析 -->
    <view class="case-section">
      <view class="case-card">
        <view class="case-header">
          <text class="case-title">案例分析</text>
        </view>
        <view class="case-content" @click="goToCaseDetail">
          <view class="case-info">
            <text class="case-name">{{ caseData.title }}</text>
            <text class="case-desc">{{ caseData.description }}</text>
            <view class="case-tags">
              <text class="case-tag" v-for="tag in caseData.tags" :key="tag">{{ tag }}</text>
            </view>
          </view>
        </view>
        <view class="case-footer" @click="goToCaseDetail">
          <text class="view-detail">查看详情 →</text>
        </view>
      </view>
    </view>

    <!-- 项目介绍 -->
    <view class="project-section">
      <view class="project-header">
        <text class="project-title">项目介绍</text>
        <text class="project-subtitle">大模块，可向下滚动</text>
      </view>
      <scroll-view class="project-scroll" scroll-y>
        <view class="project-item" v-for="(item, index) in projectList" :key="index" @click="goToProjectDetail(item)">
          <view class="project-icon-wrapper" :style="{ background: item.iconBg }">
            <text class="project-icon">{{ item.icon }}</text>
          </view>
          <view class="project-content">
            <text class="project-item-title">{{ item.title }}</text>
            <text class="project-item-desc">{{ item.description }}</text>
          </view>
          <view class="project-arrow">→</view>
        </view>
      </scroll-view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

// 案例分析数据
const caseData = ref({
  title: '大学生创新创业项目成功案例',
  description: '某团队通过平台完成项目全流程管理，最终获得省级创新创业大赛一等奖...',
  tags: ['创新创业', '项目管理', '成功案例']
})

// 项目介绍列表
const projectList = ref([
  {
    title: '风险预警',
    description: '系统根据项目进度，提前预警可能的风险',
    icon: '⚠️',
    iconBg: 'linear-gradient(135deg, #ff6b6b 0%, #ee5a6f 100%)',
    type: 'risk'
  },
  {
    title: '团队沟通',
    description: '集成聊天工具，方便团队成员讨论',
    icon: '💬',
    iconBg: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
    type: 'communication'
  },
  {
    title: '项目评估',
    description: '生成项目报告，评估项目成果和团队表现',
    icon: '📊',
    iconBg: 'linear-gradient(135deg, #daedbb 0%, #a8e063 100%)',
    type: 'evaluation'
  }
])

// 跳转到资料下载
const goToRepo = () => {
  uni.navigateTo({
    url: '/pages/repo/list'
  })
}

// 跳转到财务报销
const goToExpense = () => {
  uni.navigateTo({
    url: '/pages/expense/home'
  })
}

// 跳转到案例分析详情
const goToCaseDetail = () => {
  uni.navigateTo({
    url: '/pages/case/detail'
  })
}

// 跳转到项目详情
const goToProjectDetail = (item) => {
  uni.navigateTo({
    url: `/pages/project/detail?type=${item.type}`
  })
}
</script>

<style lang="scss" scoped>
.home-container {
  min-height: 100vh;
  background: linear-gradient(180deg, #f5f7fa 0%, #ffffff 100%);
  padding-bottom: 120rpx; // 为tabBar留出空间
}

// Logo区域
.logo-section {
  padding: 40rpx 30rpx 30rpx;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #4facfe 100%);
  border-bottom-left-radius: 40rpx;
  border-bottom-right-radius: 40rpx;
}

.logo-placeholder {
  width: 100%;
  height: 200rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 20rpx;
  backdrop-filter: blur(10px);
  border: 2rpx dashed rgba(255, 255, 255, 0.3);
}

.logo-img {
  width: 150rpx;
  height: 150rpx;
}

// 快速入口
.quick-entry-section {
  display: flex;
  gap: 20rpx;
  padding: 30rpx;
  margin-top: -20rpx;
}

.entry-card {
  flex: 1;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 24rpx;
  padding: 40rpx 20rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
  transition: all 0.3s;
}

.entry-card:active {
  transform: scale(0.95);
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.12);
}

.entry-icon {
  width: 100rpx;
  height: 100rpx;
  border-radius: 24rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 50rpx;
  margin-bottom: 20rpx;
  box-shadow: 0 6rpx 20rpx rgba(0, 0, 0, 0.15);
}

.entry-text {
  font-size: 28rpx;
  color: #333;
  font-weight: 500;
}

// 案例分析
.case-section {
  padding: 0 30rpx 30rpx;
}

.case-card {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 24rpx;
  overflow: hidden;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
}

.case-header {
  padding: 30rpx 30rpx 20rpx;
  border-bottom: 1rpx solid #f0f0f0;
}

.case-title {
  font-size: 32rpx;
  font-weight: bold;
  color: #333;
}

.case-content {
  padding: 30rpx;
}

.case-info {
  display: flex;
  flex-direction: column;
  gap: 15rpx;
}

.case-name {
  font-size: 30rpx;
  font-weight: 600;
  color: #333;
  margin-bottom: 10rpx;
}

.case-desc {
  font-size: 26rpx;
  color: #666;
  line-height: 1.6;
  margin-bottom: 15rpx;
}

.case-tags {
  display: flex;
  gap: 15rpx;
  flex-wrap: wrap;
}

.case-tag {
  font-size: 22rpx;
  color: #667eea;
  background: rgba(102, 126, 234, 0.1);
  padding: 8rpx 16rpx;
  border-radius: 12rpx;
}

.case-footer {
  padding: 20rpx 30rpx;
  border-top: 1rpx solid #f0f0f0;
  text-align: right;
}

.view-detail {
  font-size: 26rpx;
  color: #667eea;
  font-weight: 500;
}

// 项目介绍
.project-section {
  padding: 30rpx;
  background: rgba(255, 255, 255, 0.95);
  margin: 0 30rpx 30rpx;
  border-radius: 24rpx;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
}

.project-header {
  display: flex;
  flex-direction: column;
  margin-bottom: 30rpx;
  padding-bottom: 20rpx;
  border-bottom: 1rpx solid #f0f0f0;
}

.project-title {
  font-size: 32rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 8rpx;
}

.project-subtitle {
  font-size: 24rpx;
  color: #999;
}

.project-scroll {
  max-height: 800rpx;
}

.project-item {
  display: flex;
  align-items: center;
  padding: 30rpx 0;
  border-bottom: 1rpx solid #f5f5f5;
  transition: all 0.3s;
}

.project-item:last-child {
  border-bottom: none;
}

.project-item:active {
  background: #f8f8f8;
  border-radius: 16rpx;
  padding-left: 10rpx;
  padding-right: 10rpx;
}

.project-icon-wrapper {
  width: 100rpx;
  height: 100rpx;
  border-radius: 20rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 24rpx;
  box-shadow: 0 6rpx 20rpx rgba(0, 0, 0, 0.12);
}

.project-icon {
  font-size: 50rpx;
}

.project-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 10rpx;
}

.project-item-title {
  font-size: 30rpx;
  font-weight: 600;
  color: #333;
}

.project-item-desc {
  font-size: 24rpx;
  color: #666;
  line-height: 1.5;
}

.project-arrow {
  font-size: 32rpx;
  color: #ccc;
  margin-left: 20rpx;
}
</style>
