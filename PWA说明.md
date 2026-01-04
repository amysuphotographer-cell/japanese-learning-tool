# PWA 离线支持配置说明

## 📱 什么是 PWA？

PWA (Progressive Web App) 是一种可以像原生应用一样使用的网页应用。主要特点：
- ✅ 可以安装到手机/电脑主屏幕
- ✅ 支持离线使用
- ✅ 加载速度更快
- ✅ 类似原生应用的体验

## 🎯 已完成的配置

### 1. 创建的文件
- `manifest.json` - PWA 应用配置文件
- `service-worker.js` - 离线缓存管理
- `icon.svg` - 应用图标源文件
- `generate-icons.html` - 图标生成工具

### 2. 功能特性
- ✅ 离线缓存支持
- ✅ 自动检测更新
- ✅ 可添加到主屏幕
- ✅ 独立窗口运行
- ✅ 主题色配置

## 📝 生成应用图标

### 方法一：使用图标生成器（推荐）

1. 在浏览器中打开 `generate-icons.html`
2. 页面会自动生成两个尺寸的图标
3. 右键点击图标，选择"下载"
4. 将下载的文件重命名为：
   - `icon-192.png` (192x192)
   - `icon-512.png` (512x512)
5. 将图标文件放在项目根目录

### 方法二：使用在线工具

访问以下任一网站上传 `icon.svg` 生成 PNG：
- https://realfavicongenerator.net/
- https://www.pwabuilder.com/
- https://app-manifest.firebaseapp.com/

需要生成的尺寸：
- 192x192 像素
- 512x512 像素

### 方法三：使用设计软件

使用 Figma / Photoshop / Sketch 等工具：
1. 创建 512x512 画布
2. 使用渐变背景 (#667eea → #764ba2)
3. 添加白色"動"字
4. 导出为 PNG 格式（192x192 和 512x512）

## 🚀 如何使用 PWA

### 在手机上安装（以 Chrome 为例）

1. 用手机浏览器访问应用
2. 点击浏览器菜单（三个点）
3. 选择"添加到主屏幕"或"安装应用"
4. 从主屏幕打开即可离线使用

### 在电脑上安装

**Chrome:**
1. 访问应用网址
2. 地址栏右侧会出现安装图标 ⊕
3. 点击安装
4. 应用会在独立窗口打开

**Edge:**
- 类似 Chrome 的操作

**Safari (macOS):**
- 暂不完全支持，但仍可离线缓存

## 🔧 配置说明

### manifest.json 配置项

```json
{
  "name": "应用完整名称",
  "short_name": "应用短名称（主屏幕显示）",
  "start_url": "启动路径",
  "display": "显示模式（standalone = 独立窗口）",
  "theme_color": "主题色",
  "background_color": "启动背景色"
}
```

### Service Worker 缓存策略

当前使用的策略：**缓存优先，网络回退**
- 优先从缓存读取
- 缓存未命中时从网络获取
- 网络请求成功后更新缓存
- 完全离线时使用缓存

## 📊 离线功能测试

### 测试步骤

1. 首次访问应用（联网状态）
2. 打开浏览器开发者工具（F12）
3. 切换到 Application/应用 标签
4. 查看 Service Workers 是否已注册
5. 勾选 "Offline" 模拟离线状态
6. 刷新页面，应用仍可正常使用

### 验证缓存

在开发者工具中：
1. Application → Cache Storage
2. 查看是否有缓存数据
3. 可以手动清除测试

## ⚠️ 注意事项

1. **HTTPS 要求**
   - PWA 必须在 HTTPS 环境下运行
   - localhost 例外（开发测试用）
   - GitHub Pages 自动支持 HTTPS

2. **浏览器兼容性**
   - Chrome/Edge: 完全支持 ✅
   - Firefox: 部分支持 ⚠️
   - Safari: 有限支持 ⚠️
   - iOS Safari 16+: 较好支持 ✅

3. **缓存更新**
   - 修改代码后需要更新 Service Worker 版本号
   - 在 `service-worker.js` 中修改 `CACHE_NAME`
   - 用户下次访问时会提示更新

4. **调试建议**
   - 使用无痕模式测试
   - 及时清除缓存
   - 查看控制台日志

## 🔄 更新缓存版本

当你修改了代码后：

1. 打开 `service-worker.js`
2. 修改第一行的版本号：
   ```javascript
   const CACHE_NAME = 'japanese-verb-learning-v1.2'; // 增加版本号
   ```
3. 用户下次访问时会自动提示更新

## 📱 用户体验优化建议

- 首次加载会缓存所有资源
- 后续访问几乎瞬间加载
- 完全离线也能使用
- 更新时自动提示用户刷新

## 🎉 成功标志

安装成功后，你会看到：
- ✅ 主屏幕有应用图标
- ✅ 独立窗口运行（无浏览器地址栏）
- ✅ 离线状态下仍可使用
- ✅ 加载速度显著提升

---

生成日期：2026-01-04
