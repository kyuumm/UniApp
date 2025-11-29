# TabBar 图标配置指南

## 问题说明

由于无法直接创建图片文件，tabBar 的图标需要手动添加。

## 解决方案

### 方案1：使用在线图标生成工具（推荐）

1. 访问图标网站（如 iconfont.cn 或 iconify.design）
2. 搜索"首页"和"我的"相关的图标
3. 下载 81px × 81px 的 PNG 图标
4. 将图标保存到 `src/static/tabbar/` 目录：
   - `home.png` - 首页未选中图标（灰色）
   - `home-active.png` - 首页选中图标（主题色 #667eea）
   - `me.png` - 我的未选中图标（灰色）
   - `me-active.png` - 我的选中图标（主题色 #667eea）

### 方案2：临时使用纯文字 TabBar

如果暂时没有图标，可以修改 `src/pages.json`，将 tabBar 配置改为：

```json
"tabBar": {
  "color": "#999999",
  "selectedColor": "#667eea",
  "backgroundColor": "#ffffff",
  "borderStyle": "white",
  "list": [
    {
      "pagePath": "pages/index/index",
      "text": "首页"
    },
    {
      "pagePath": "pages/me/index",
      "text": "我的"
    }
  ]
}
```

**注意：** 移除 `iconPath` 和 `selectedIconPath` 配置后，tabBar 将只显示文字（某些平台可能不支持）。

### 方案3：使用现有 Logo

可以临时使用项目中的 `logo.png` 作为占位图标（需要调整大小）。

## 图标要求

- **尺寸：** 81px × 81px（推荐）
- **格式：** PNG（支持透明背景）
- **颜色：**
  - 未选中：灰色 (#999999)
  - 选中：主题色 (#667eea)
- **风格：** 简洁的线条图标，与整体 UI 风格一致

## 快速测试

添加图标后，运行项目即可看到底部导航栏。如果图标路径不正确，uniapp 会在控制台显示错误信息。

