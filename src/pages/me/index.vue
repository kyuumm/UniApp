<template>
  <view class="me">
    <!-- 头部 -->
    <view class="banner">
      <view class="avatar">{{ initial }}</view>
      <view class="meta">
        <view class="name">{{ userInfo.name || '未登录' }}</view>
        <view class="role">{{ userInfo.role || '游客' }}</view>
      </view>
    </view>

    <!-- 分组卡 -->
    <view class="section">
      <view class="sec-hd">我的内容</view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(244 250 255) 0%, rgb(0, 219, 222) 100%);">◆</view><text class="txt">我的下载</text><text class="arr">›</text></view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(255 249 231) 0%, rgb(255, 154, 86) 100%);">◆</view><text class="txt">我的收藏</text><text class="arr">›</text></view>
    </view>

    <view class="section">
      <view class="sec-hd">项目管理</view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%);">◆</view><text class="txt">我的项目</text><text class="arr">›</text></view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%);">◆</view><text class="txt">我的报表</text><text class="arr">›</text></view>
    </view>

    <view class="section">
      <view class="sec-hd">财务报销</view>
      <view class="item" @click="goExpense"><view class="ico" style="background:linear-gradient(135deg, rgb(255 249 231) 0%, rgb(255, 154, 86) 100%);">◆</view><text class="txt">手机报销</text><text class="arr">›</text></view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(244 250 255) 0%, rgb(0, 219, 222) 100%);">◆</view><text class="txt">电子发票</text><text class="arr">›</text></view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%);">◆</view><text class="txt">报销分析</text><text class="arr">›</text></view>
    </view>

    <view class="section" v-if="userInfo.role==='admin'">
      <view class="sec-hd">管理员</view>
      <view class="item" @click="todo"><view class="ico" style="background:linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%);">◆</view><text class="txt">管理后台</text><text class="arr">›</text></view>
    </view>

    <view class="pad" />
    <view class="logout"><button class="btn" @click="logout">退出登录</button></view>
    <!-- 自定义TabBar -->
    <custom-tabbar />
  </view>
</template>

<script setup>
import { computed, ref } from 'vue'
import { onShow } from '@dcloudio/uni-app'
import CustomTabbar from '../../components/custom-tabbar/index.vue'
const userInfo = ref({ name:'张三', role:'student' })
const initial = computed(()=> (userInfo.value.name?.[0] || 'U'))

// 页面显示时更新TabBar状态
onShow(() => {
  uni.$emit('updateTabBar', 1)
})

const todo = () => uni.showToast({ title:'功能开发中', icon:'none' })
const goExpense = () => uni.navigateTo({ url:'/pages/expense/home' })
const logout = () => {
  uni.showModal({
    title:'提示', content:'确定要退出登录吗？',
    success: r => { if (r.confirm) uni.reLaunch({ url:'/pages/login/login' }) }
  })
}
</script>

<style lang="scss" scoped>
.me{ min-height:100vh; background:linear-gradient(180deg,#e6f3ff 0%,#f7fbff 100%); padding-bottom:120rpx; }

.banner{
  display:flex;align-items:center;gap:20rpx; padding:48rpx 28rpx 28rpx;
  background:linear-gradient(135deg,#e8f3ff 0%,#f5fbff 100%);
  border-bottom-left-radius:32rpx;border-bottom-right-radius:32rpx;
}
.avatar{
  width:112rpx;height:112rpx;border-radius:26rpx;background:linear-gradient(135deg,#4facfe 0%,#00dbde 100%);
  color:#fff;font-weight:800;font-size:44rpx;display:flex;align-items:center;justify-content:center;
  box-shadow:0 12rpx 36rpx rgba(31,141,242,.25);
}
.meta{ display:flex;flex-direction:column;gap:6rpx; }
.name{ font-size:34rpx;font-weight:800;color:#0f172a; }
.role{ font-size:24rpx;color:#475569;background:#eef6ff;border-radius:999rpx;padding:6rpx 16rpx; width: auto; display:inline-block; }

.section{ background:#fff; margin:18rpx 28rpx; border-radius:22rpx; overflow:hidden;
  box-shadow:0 14rpx 40rpx rgba(31,141,242,.08);
}
.sec-hd{ font-size:26rpx;color:#64748b;padding:24rpx 24rpx 10rpx;border-bottom:1rpx solid #eef2f7; }
.item{ display:flex;align-items:center;padding:26rpx 24rpx;border-bottom:1rpx solid #f3f6fa; }
.item:last-child{ border-bottom:none; }
.ico{ width:80rpx;height:80rpx;border-radius:18rpx; display:flex;align-items:center;justify-content:center;
  font-size:44rpx;color:#fff; margin-right:16rpx; box-shadow:0 10rpx 24rpx rgba(0,0,0,.08); }
.txt{ flex:1;font-size:30rpx;color:#0f172a; }
.arr{ color:#94a3b8; font-size:36rpx; }

.logout{ padding: 10rpx 28rpx 28rpx; }
.btn{
  width:100%;height:96rpx;border-radius:48rpx;border:2rpx solid #ff6b6b;
  color:#ff6b6b;background:#fff;font-size:30rpx;font-weight:700;
}
.btn:active{ background:#fff5f5; }
.pad{ height: 40rpx; }
</style>
