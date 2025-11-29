<template>
  <view class="login-container">
    <!-- 背景装饰 -->
    <view class="bg-decoration">
      <view class="bg-circle circle-1"></view>
      <view class="bg-circle circle-2"></view>
      <view class="bg-circle circle-3"></view>
    </view>

    <!-- 内容 -->
    <view class="content-wrapper">
      <!-- Logo + 标题 -->
      <view class="header-section">
        <view class="logo-wrapper">
          <view class="logo-icon">创</view>
        </view>
        <text class="app-title">创空间</text>
        <text class="app-subtitle">高校创新创业一站式平台</text>
      </view>

      <!-- 表单 -->
      <view class="form-section">
        <view class="form-title">登录创空间</view>

        <view class="input-wrapper">
          <view class="input-icon">用户名</view>
          <input
            class="input-field"
            type="text"
            placeholder="请输入账号 / 学号"
            v-model="formData.username"
            placeholder-style="color:#9aa3af"
          />
        </view>

        <view class="input-wrapper">
          <view class="input-icon">密码</view>
          <input
            class="input-field"
            type="password"
            placeholder="请输入密码"
            v-model="formData.password"
            placeholder-style="color:#9aa3af"
          />
        </view>

        <button class="primary-btn" @click="handleLogin">登录</button>

        <view class="register-link">
          <text class="register-text">还没有账号？</text>
          <text class="link-btn" @click="goToRegister">立即注册</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

const formData = ref({ username: '', password: '' })

const handleLogin = () => {
  if (!formData.value.username) {
    return uni.showToast({ title: '请输入账号', icon: 'none' })
  }
  if (!formData.value.password) {
    return uni.showToast({ title: '请输入密码', icon: 'none' })
  }
  uni.showToast({ title: '登录成功', icon: 'success' })
  setTimeout(() => {
    uni.reLaunch({ url: '/pages/index/index' })
  }, 800)
}

const goToRegister = () => {
  uni.navigateTo({ url: '/pages/register/register' })
}
</script>

<style lang="scss" scoped>
// ==== 主题色（可抽到 global.scss 复用） ====
$brand-start: #4facfe;   // 天空蓝
$brand-end:   #00dbde;   // 青绿
$brand-deep:  #1f8df2;   // 蓝色文字/按钮悬停
$accent:      #ffc46b;   // 温暖点缀（参考图里的暖色小卡片）
$bg-top:      #e6f3ff;   // 顶部淡蓝背景
$bg-bottom:   #f7fbff;

// 页面背景：淡蓝 → 近白，弱化紫色
.login-container {
  min-height: 100vh;
  background: linear-gradient(180deg, $bg-top 0%, $bg-bottom 100%);
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40rpx;
}

.bg-decoration {
  position: absolute; inset: 0; z-index: 0; overflow: hidden;
}
.bg-circle {
  position: absolute; border-radius: 50%;
  background: rgba(255,255,255,0.5);
  filter: blur(2px);
}
.circle-1 { width: 440rpx; height: 440rpx; top: -120rpx; right: -140rpx; opacity: .6; }
.circle-2 { width: 320rpx; height: 320rpx; bottom: -80rpx; left: -80rpx; opacity: .45; }
.circle-3 { width: 220rpx; height: 220rpx; top: 46%; left: 8%; opacity: .35; }

.content-wrapper { width: 100%; max-width: 640rpx; position: relative; z-index: 1; }

.header-section { text-align: center; margin-bottom: 64rpx; }
.logo-wrapper { margin-bottom: 24rpx; }
.logo-icon {
  width: 120rpx; height: 120rpx; border-radius: 28rpx;
  background: linear-gradient(135deg, $brand-start 0%, $brand-end 100%);
  color: #fff; display: flex; align-items: center; justify-content: center;
  font-size: 44rpx; font-weight: 800;
  box-shadow: 0 12rpx 36rpx rgba(31, 141, 242, 0.25);
}
.app-title {
  display: block; font-size: 48rpx; font-weight: 800; color: #0f172a;  // 更深更稳
  margin-bottom: 8rpx;
}
.app-subtitle { display: block; font-size: 26rpx; color: #475569; }

.form-section {
  background: #ffffff;
  border-radius: 32rpx;
  padding: 56rpx 48rpx;
  box-shadow: 0 24rpx 68rpx rgba(31, 141, 242, 0.08);
  backdrop-filter: blur(6px);
}
.form-title {
  font-size: 36rpx; font-weight: 700; color: #0f172a; text-align: center; margin-bottom: 40rpx;
}

.input-wrapper {
  display: flex; align-items: center;
  background: #f3f6fb; border-radius: 20rpx; padding: 0 28rpx;
  margin-bottom: 28rpx; height: 96rpx; transition: background .2s;
}
.input-wrapper:active { background: #eaf0f8; }
.input-icon { font-size: 34rpx; margin-right: 18rpx; }
.input-field { flex: 1; font-size: 28rpx; color: #0f172a; height: 100%; }

.primary-btn {
  width: 100%; height: 96rpx; border-radius: 48rpx; border: none;
  background: linear-gradient(135deg, $brand-start 0%, $brand-end 100%);
  color: #fff; font-size: 32rpx; font-weight: 700; margin-top: 12rpx;
  box-shadow: 0 14rpx 34rpx rgba(31, 141, 242, .28);
  display: flex; align-items: center; justify-content: center;
}
.primary-btn:active { transform: scale(.985); opacity: .95; }

.register-link { display:flex; justify-content:center; align-items:center; margin-top: 36rpx; }
.register-text { font-size: 26rpx; color: #6b7280; margin-right: 10rpx; }
.link-btn { font-size: 26rpx; color: $brand-deep; font-weight: 700; }
.link-btn:active { opacity: .75; }
</style>
