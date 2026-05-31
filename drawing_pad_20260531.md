# 任务工件：初代iPhone风格手绘板页面

## 任务目标
创建一个给手机使用的二维码艺术页面，实现手绘板和图像↔文本转换功能，采用初代iPhone立体按钮风格，仅使用黑白灰无色系。

## 核心需求
1. 第一个页面大部分是手绘板，支持触屏手绘
2. 页面下方有按钮，点击可将图像转码成满屏文本数据，再次点击返回图像
3. UI按钮采用初代iPhone立体风格
4. UI颜色限定黑白灰无色系
5. 用户无私人服务器，需纯前端实现

## 方案选择
采用**方案1：基础版 - Base64编码转换**
- 使用Canvas API实现手绘板
- 切换时将Canvas图像转为Base64字符串填满屏幕
- 再次切换时从Base64还原图像
- 初代iPhone风格的立体按钮(使用CSS渐变和阴影实现)

## 技术实现

### 文件位置
`C:\Users\22776\.qclaw\workspace-agent-a43f54b3\drawing_pad.html`

### 核心功能
1. **Canvas手绘板**
   - 支持鼠标和触摸事件
   - 白色画笔，黑色背景
   - 线条宽度3px，圆润笔触
   - 自动适应屏幕尺寸

2. **图像↔文本切换**
   - 使用`canvas.toDataURL('image/png')`生成Base64编码
   - 切换时显示模式指示器动画
   - 文本模式显示完整的Base64字符串
   - 再次切换返回手绘模式

3. **初代iPhone立体按钮**
   - 使用多层渐变和阴影实现立体效果
   - 按下时有下沉动画效果
   - 顶部有高光条模拟塑料质感
   - 灰黑色系，符合初代iPhone风格

4. **UI设计**
   - 顶部状态栏：渐变灰色，显示当前模式
   - 手绘区域：纯黑背景，白色画笔
   - 底部按钮区：渐变灰色背景
   - 文本显示区：黑色背景，白色等宽字体

### 关键代码逻辑
```javascript
// 切换到文本模式
base64Data = canvas.toDataURL('image/png');
canvasContainer.style.display = 'none';
textDisplay.style.display = 'block';
textDisplay.textContent = base64Data;

// 切换回手绘模式
canvasContainer.style.display = 'block';
textDisplay.style.display = 'none';
```

## 使用说明
1. 在手机浏览器中打开`drawing_pad.html`
2. 使用手指在黑色区域绘制
3. 点击底部"转换为文本"按钮，查看Base64编码
4. 点击"返回手绘"按钮，返回绘制界面
5. 双击画布可清除内容

## 设计亮点
1. **纯前端实现**：无需服务器，可本地打开使用
2. **响应式设计**：自动适应手机屏幕
3. **初代iPhone风格**：完美还原2007年初代iPhone的立体按钮质感
4. **黑白灰无色系**：严格遵循用户指定的色彩限制
5. **流畅交互**：切换时有动画提示，体验顺滑

## 技术要点
- 使用`touch-action: none`防止触摸时页面滚动
- 使用`user-select: none`防止文本选择
- Canvas事件同时支持鼠标和触摸
- Base64编码完整保留图像数据，可无损还原

## 后续优化方向
如需进一步增强，可考虑：
- 方案2的ASCII艺术转换
- 方案3的增强功能（保存、分享、笔刷设置等）
- 添加更多初代iPhone UI元素（如滑动解锁等）
