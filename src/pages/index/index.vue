<template>

  <view class="home">
    <!-- 顶部 Logo/横幅 -->
    <view class="hero">
      <view class="hero-box">
  <image class="logo" :src="logoUrl" mode="aspectFit" />
        <view class="slogan">创空间 · 高校创新创业一站式平台</view>
      </view>
    </view>

    <!-- 快速入口 -->
    <view class="grid">
      <view class="tile" @click="goToRepo">
        <view class="tile-icon" style="background:linear-gradient(135deg, rgb(244 250 255) 0%, rgb(0, 219, 222) 100%);">◆</view>
        <view class="tile-text">资料下载</view>
      </view>
      <view class="tile" @click="goToExpense">
        <view class="tile-icon" style="background:linear-gradient(135deg, rgb(255 249 231) 0%, rgb(255, 154, 86) 100%);">◆</view>
        <view class="tile-text">财务报销</view>
      </view>
    </view>

    <!-- 案例预览（只展示一条） -->
    <view class="card">
      <view class="card-hd">
        <text class="card-title">案例分析</text>
        <text class="link" @click="goToCaseDetail">查看详情 →</text>
      </view>
      <view class="card-bd" @click="goToCaseDetail">
        <view class="case-name ellipsis-1">{{ caseData.title }}</view>
        <view class="case-desc ellipsis-2">{{ caseData.description }}</view>
        <view class="tags">
          <text class="tag" v-for="t in caseData.tags" :key="t">{{ t }}</text>
        </view>
      </view>
    </view>

    <!-- 项目介绍（三张竖排卡片，可点击） -->
    <view class="card">
      <view class="card-hd">
        <text class="card-title">项目介绍</text>
        <text class="sub">关键能力一览</text>
      </view>
      <view class="proj-list">
        <view class="proj-item" v-for="it in projectList" :key="it.type" @click="goToProjectDetail(it)">
          <view class="proj-icon" :style="{background: it.iconBg}">{{ it.icon }}</view>
          <view class="proj-main">
            <view class="proj-title ellipsis-1">{{ it.title }}</view>
            <view class="proj-desc ellipsis-2">{{ it.description }}</view>
          </view>
          <text class="arrow">›</text>
        </view>
      </view>
    </view>

    <view class="safe-bottom" />
    <!-- 自定义TabBar -->
    <custom-tabbar />
  </view>
</template>

<script setup>
import { ref } from 'vue'
import { onShow } from '@dcloudio/uni-app'
import CustomTabbar from '../../components/custom-tabbar/index.vue'


import logoUrl from '@/static/logo.png'   //logo图片

// 页面显示时更新TabBar状态
onShow(() => {
  uni.$emit('updateTabBar', 0)
})

// 案例死数据
const caseData = ref({
  title: '省赛一等奖：校园碳中和协同管理平台',
  description: '团队基于创空间完成资料沉淀、项目里程碑管理与导师协作，最终在省赛中获得一等奖…',
  tags: ['创新创业','项目管理','低碳']
})

// 三个项目卡（死数据）
const projectList = ref([
  { type:'risk', title:'AI 校园闲置物品匹配系统', icon:'◆',
    description:'依托 AI 算法实现校园闲置物品供需智能匹配，提供价格评估、物流配送、信用担保等服务，开设 “以物换物” 专区，已完成校内小规模测试，匹配成功率超 85%。',
    iconBg:'linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%)'
  },
  { type:'communication', title:'非遗文化数字化传播平台', icon:'◆',
    description:'联合非遗传承人开发线上课程，打造 3D 交互式数字展厅，提供手作材料包购买与线下体验课预约服务，校内参与学生超 2000 人次。',
    iconBg:'linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%)'
  },
  { type:'evaluation', title:'校园智慧自习室管理系统', icon:'◆',
    description:'通过物联网技术实现自习室座位预约、实时监控，集成环境监测、自助充电等功能，落地后将座位利用率从 60% 提升至 90%',
    iconBg:'linear-gradient(135deg, rgb(79, 172, 254) 0%, rgb(243 243 243) 100%)'
  }
])

const goToRepo = () => uni.navigateTo({ url:'/pages/repo/list' })
const goToExpense = () => uni.navigateTo({ url:'/pages/expense/home' })
const goToCaseDetail = () => uni.navigateTo({ url:'/pages/case/detail' })
const goToProjectDetail = (it) => uni.navigateTo({ url:`/pages/project/detail?type=${it.type}` })
</script>

<style lang="scss" scoped>
// 主题色（蓝-青）
$brand-deep:  #0f172a;
$brand-blue:  #4facfe;
$brand-teal:  #00dbde;
$muted:       #64748b;

.home{
  min-height:100vh;background:linear-gradient(180deg,#e6f3ff 0%,#f7fbff 100%);
  padding-bottom:120rpx;
}
.safe-bottom{ height: env(safe-area-inset-bottom); }

// 顶部横幅
.hero{ padding: 32rpx 28rpx 24rpx; border-bottom-left-radius:36rpx;border-bottom-right-radius:36rpx;
  background: linear-gradient(135deg,#e8f3ff 0%,#f5fbff 100%);
}
.hero-box{  border-radius:24rpx; padding:28rpx; 
//box-shadow:0 0.4375rem 1.25rem rgb(112 159 210);
  display:flex; align-items:center; gap:20rpx;
}
.logo{ width:120rpx; height:120rpx; border-radius:16rpx; }
.slogan{ color:$brand-deep; font-size:28rpx; font-weight:700; }

// 两宫格
.grid{ display:flex; gap:20rpx; padding:24rpx 28rpx; }
.tile{
  flex:1;background:#fff;border-radius:24rpx;padding:30rpx 20rpx; text-align:center;
  box-shadow:0 10rpx 28rpx rgba(31,141,242,.08); transition:transform .15s ease;
}
.tile:active{ transform:scale(.98); }
.tile-icon{
  width:96rpx;height:96rpx;border-radius:22rpx;display:flex;align-items:center;justify-content:center;
  font-size:48rpx;margin:0 auto 14rpx; color:#fff; box-shadow:0 10rpx 24rpx rgba(0,0,0,.12);
}
.tile-text{ font-size:28rpx; color:$brand-deep; font-weight:600; }

// 通用卡片
.card{ background:#fff;border-radius:24rpx;margin:0 28rpx 24rpx; box-shadow:0 14rpx 40rpx rgba(31,141,242,.08); }
.card-hd{ display:flex;align-items:center;justify-content:space-between; padding:26rpx 26rpx 12rpx;
  border-bottom:1rpx solid #eef2f7;
}
.card-title{ font-size:30rpx; font-weight:800; color:$brand-deep; }
.sub{ font-size:24rpx; color:#94a3b8; }
.link{ font-size:24rpx; color:#1f8df2; }

.card-bd{ padding:22rpx 26rpx 26rpx; }
.tags{ display:flex; gap:12rpx; flex-wrap:wrap; margin-top:8rpx; }
.tag{ font-size:22rpx; color:#1f8df2; background:rgba(31,141,242,.08); padding:6rpx 14rpx; border-radius:12rpx; }

.ellipsis-1{ overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
.ellipsis-2{ display:-webkit-box; -webkit-line-clamp:2; -webkit-box-orient:vertical; overflow:hidden; }

.case-name{ font-size:30rpx; font-weight:700; color:$brand-deep; margin-bottom:6rpx; }
.case-desc{ font-size:26rpx; color:$muted; }

// 项目卡竖排列表
.proj-list{ padding: 8rpx 8rpx 14rpx; }
.proj-item{
  display:flex; align-items:flex-start; gap:18rpx; padding:22rpx; border-radius:20rpx; background:#f7fbff;
  transition:background .15s; margin:12rpx 8rpx;
}
.proj-item:active{ background:#eef6ff; }
.proj-icon{ width:88rpx;height:88rpx;border-radius:18rpx; color:#fff; font-size:44rpx;
  display:flex; align-items:center; justify-content:center; box-shadow:0 10rpx 24rpx rgba(0,0,0,.1);
}
.proj-main{ flex:1; }
.proj-title{ font-size:30rpx; font-weight:700; color:$brand-deep; margin-bottom:4rpx; }
.proj-desc{ font-size:26rpx; color:$muted; }
.arrow{ align-self:center; color:#94a3b8; font-size:36rpx; }
</style>
