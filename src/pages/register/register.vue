<template>
  <view class="register-container">
    <view class="bg-decoration">
      <view class="bg-circle circle-1"></view>
      <view class="bg-circle circle-2"></view>
      <view class="bg-circle circle-3"></view>
    </view>

    <view class="content-wrapper">
      <view class="header-section">
        <view class="logo-wrapper">
          <view class="logo-icon">创</view>
        </view>
        <text class="app-title">创空间</text>
        <text class="app-subtitle">创建你的创新创业账号</text>
      </view>

      <view class="form-section">
        <view class="form-title">注册创空间</view>

        <view class="input-wrapper">
          <view class="input-icon">用户名</view>
          <input
            class="input-field"
            type="text"
            placeholder="请输入账号（6–20位）"
            v-model="formData.username"
            placeholder-style="color:#9aa3af"
            maxlength="20"
          />
        </view>

        <view class="input-wrapper">
          <view class="input-icon">密码</view>
          <input
            class="input-field"
            type="password"
            placeholder="请输入密码（至少6位）"
            v-model="formData.password"
            placeholder-style="color:#9aa3af"
            maxlength="20"
          />
        </view>

        <view class="input-wrapper">
          <view class="input-icon">验证</view>
          <input
            class="input-field"
            type="password"
            placeholder="请再次输入密码"
            v-model="formData.confirmPassword"
            placeholder-style="color:#9aa3af"
            maxlength="20"
          />
        </view>

        <button class="primary-btn" @click="handleRegister">注册</button>

        <view class="login-link">
          <text class="login-text">已有账号？</text>
          <text class="link-btn" @click="goToLogin">去登录</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'
const formData = ref({ username: '', password: '', confirmPassword: '' })

const handleRegister = () => {
  if (!formData.value.username) return uni.showToast({ title: '请输入账号', icon: 'none' })
  if (formData.value.username.length < 6 || formData.value.username.length > 20)
    return uni.showToast({ title: '账号长度为6-20位', icon: 'none' })

  if (!formData.value.password) return uni.showToast({ title: '请输入密码', icon: 'none' })
  if (formData.value.password.length < 6)
    return uni.showToast({ title: '密码至少6位', icon: 'none' })

  if (!formData.value.confirmPassword)
    return uni.showToast({ title: '请再次输入密码', icon: 'none' })
  if (formData.value.password !== formData.value.confirmPassword)
    return uni.showToast({ title: '两次密码不一致', icon: 'none' })

  uni.showToast({ title: '注册成功', icon: 'success' })
  setTimeout(() => uni.navigateBack(), 800)
}

const goToLogin = () => uni.navigateBack()
</script>

<style lang="scss" scoped>
// 与登录页保持一致的主题变量
$brand-start: #4facfe;
$brand-end:   #00dbde;
$brand-deep:  #1f8df2;
$bg-top:      #e6f3ff;
$bg-bottom:   #f7fbff;

.register-container {
  min-height: 100vh;
  background: linear-gradient(180deg, $bg-top 0%, $bg-bottom 100%);
  position: relative; overflow: hidden;
  display: flex; align-items: center; justify-content: center;
  padding: 40rpx;
}
.bg-decoration { position:absolute; inset:0; z-index:0; overflow:hidden; }
.bg-circle { position:absolute; border-radius:50%; background: rgba(255,255,255,.5); filter: blur(2px); }
.circle-1 { width: 440rpx; height:440rpx; top:-120rpx; right:-140rpx; opacity:.6; }
.circle-2 { width: 320rpx; height:320rpx; bottom:-80rpx; left:-80rpx; opacity:.45; }
.circle-3 { width: 220rpx; height:220rpx; top:46%; left:8%; opacity:.35; }

.content-wrapper { width:100%; max-width:640rpx; position:relative; z-index:1; }
.header-section { text-align:center; margin-bottom:60rpx; }
.logo-wrapper { margin-bottom:24rpx; }
.logo-icon {
  width:120rpx; height:120rpx; border-radius:28rpx;
  background: linear-gradient(135deg, $brand-start 0%, $brand-end 100%);
  color:#fff; display:flex; align-items:center; justify-content:center;
  font-size:44rpx; font-weight:800;
  box-shadow: 0 12rpx 36rpx rgba(31,141,242,.25);
}
.app-title { display:block; font-size:48rpx; font-weight:800; color:#0f172a; margin-bottom:8rpx; }
.app-subtitle { display:block; font-size:26rpx; color:#475569; }

.form-section {
  background:#fff; border-radius:32rpx; padding:56rpx 48rpx;
  box-shadow: 0 24rpx 68rpx rgba(31,141,242,.08); backdrop-filter: blur(6px);
}
.form-title { font-size:36rpx; font-weight:700; color:#0f172a; text-align:center; margin-bottom:40rpx; }

.input-wrapper {
  display:flex; align-items:center; background:#f3f6fb;
  border-radius:20rpx; padding:0 28rpx; margin-bottom:28rpx; height:96rpx;
}
.input-wrapper:active { background:#eaf0f8; }
.input-icon { font-size:34rpx; margin-right:18rpx; }
.input-field { flex:1; font-size:28rpx; color:#0f172a; height:100%; }

.primary-btn {
  width:100%; height:96rpx; border-radius:48rpx; border:none;
  background: linear-gradient(135deg, $brand-start 0%, $brand-end 100%);
  color:#fff; font-size:32rpx; font-weight:700; margin-top:12rpx;
  box-shadow: 0 14rpx 34rpx rgba(31,141,242,.28);
  display:flex; align-items:center; justify-content:center;
}
.primary-btn:active { transform: scale(.985); opacity:.95; }

.login-link { display:flex; justify-content:center; align-items:center; margin-top:36rpx; }
.login-text { font-size:26rpx; color:#6b7280; margin-right:10rpx; }
.link-btn { font-size:26rpx; color:$brand-deep; font-weight:700; }
.link-btn:active { opacity:.75; }
</style>
