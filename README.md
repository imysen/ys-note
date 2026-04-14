# 云森的笔记本  

> 在这里收集一下在互联网各个角落发掘的奇淫技巧，整理一些干货，可能用不到但不想失去的资料  

[Github](https://github.com/imysen) | [博客](https://blog.imysen.com) | [B站](https://space.bilibili.com/1212178922)

### 字体分片
1. 下载字体文件（woff2/ttf）。 （例如[LXGW文楷](https://github.com/lxgw/LxgwWenKai/releases)）
2. 根据需求选择字重：`Light`（细体）、`Regular`（正常）、`Medium`（偏粗）。  
3. 在线分片工具：[https://chinese-font.netlify.app/zh-cn/online-split/](https://chinese-font.netlify.app/zh-cn/online-split/)。  
4. 将 `.ttf` 文件拖入页面，自动转换为 `CSS` 和 `WOFF2` 文件。  

### Transfonter在线字体编辑
[Transfonter](https://transfonter.org/)
![alt text](https://cfimgbed-cncdn.236668.xyz/file/1772224939733.webp)

### 拟物毛玻璃风格提示语
''' 
正在优化工具选择...这里为你总结了一段可以直接喂给任何 AI 的**“iOS 26 拟物玻璃风（Glassmorphism + 3D 动效）”**标准提示词模板，里面包含了设计核心规范和我们在本项目中打磨好的标准示范代码。

你可以把下面的内容保存起来，在其他项目里直接发给 AI 让他照着写：

***

# 📋 复制以下提示词发送给 AI：

```markdown
你现在是一个顶尖的 UI/UX 前端开发工程师。请帮我编写一段前端代码（Vue/React/纯HTML+CSS均可），整体界面需要严格参照 **“iOS 26 未来的拟物毛玻璃风格（Glassmorphism）与 3D 空间动态响应”** 进行设计。

请严格遵守以下 5 个核心设计规范：
1. **极致毛玻璃（Material）**：使用 `backdrop-filter: blur(24px) saturate(150%)`，并在深浅色背景上保持极佳的通透感。
2. **拟真边缘光（Lighting）**：通过不对称的半透明边框（如顶部和左侧更亮）模拟顶部光源打在玻璃切角上的反光：`border-top: 1px solid rgba(255, 255, 255, 0.8)`。
3. **空间悬浮阴影（Shadows）**：拒绝扁平，使用多层 `box-shadow` 组合，必须包括“大范围环境阴影”、“高亮边缘外发光”以及“内部边缘的 inset 反射”。
4. **3D 景深物理交互（Interaction）**：鼠标悬停时，不要只做缩放，必须带上 `perspective(500px)` 和 `rotateX / rotateY`，模拟被按压或视差倾斜的空间感。
5. **苹果级弹性阻尼动效（Motion）**：入场必须使用带回弹的 `cubic-bezier(0.175, 0.885, 0.32, 1.08)`，Hover 过渡必须使用长衰减平滑曲线 `cubic-bezier(0.1, 0.9, 0.2, 1)`。

以下是该风格的标准「主按钮」和「动效」的 **参考示范代码**，请仔细学习其中的参数并在接下来的代码中复用这种质感,精准生成 `backdrop-filter` 模糊度、高级反光边框、复合 `box-shadow` 以及顺滑带回弹的 3D Hover 倾斜效果等：

```css
/* 1. 基础按钮形态结构 */
.hero-btn {
  border-radius: 999px; /* 经典药丸圆角 */
  padding: 0.7rem 1.8rem;
  cursor: pointer;
  /* 延长动画时间，保持起手快、后段平滑衰减的高级手感 */
  transition: all 0.6s cubic-bezier(0.1, 0.9, 0.2, 1);
  /* 统一设定 3D 变换基准 */
  transform: perspective(500px) rotateX(0deg) rotateY(0deg) scale(1) translateY(0);
}

/* 2. 核心毛玻璃按键质感 (主按钮) */
.btn-primary {
  /* 微渐变的半透明白光底色 */
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.6) 0%, rgba(255, 255, 255, 0.15) 100%);
  /* 模拟物理反光：顶部和左侧偏亮 */
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-top: 1px solid rgba(255, 255, 255, 0.8);
  border-left: 1px solid rgba(255, 255, 255, 0.6);
  color: #111;
  /* 核心：模糊与高饱和叠层 */
  backdrop-filter: blur(24px) saturate(150%);
  -webkit-backdrop-filter: blur(24px) saturate(150%);
  /* 组合阴影：环境阴影 + 内部微光 + 内部暗角 */
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.12), 
    inset 0 4px 6px -2px rgba(255, 255, 255, 0.9), 
    inset 0 -4px 6px -2px rgba(0, 0, 0, 0.05);
}

/* 3. 3D 浮动手感 (Hover 态) */
.btn-primary:hover {
  /* 提亮底色与边框反光 */
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.85) 0%, rgba(255, 255, 255, 0.35) 100%);
  border-top: 1px solid rgba(255, 255, 255, 1);
  border-left: 1px solid rgba(255, 255, 255, 1);
  /* 关键核心：3D偏转与放大，给人悬浮按压感 */
  transform: perspective(500px) rotateX(4deg) rotateY(-2deg) scale(1.02) translateY(-1px);
  /* 扩散外阴影，追加外部泛光边缘和更强的内发光 */
  box-shadow: 
    0 15px 40px rgba(0, 0, 0, 0.2),
    0 0 20px rgba(255, 255, 255, 0.6),
    inset 0 0 15px rgba(255, 255, 255, 0.9),
    inset 0 -4px 6px -2px rgba(0, 0, 0, 0.05);
}

/* 4. 出场弹性动画示范 */
@keyframes slideInLeft {
  0% {
    opacity: 0;
    transform: perspective(500px) translateX(-40px) rotateY(-15deg);
  }
  100% {
    opacity: 1;
    transform: perspective(500px) translateX(0) rotateY(0deg);
  }
}

/* 使用示例：配置 backwords 以及超量回弹曲线 */
.animated-element {
  animation: slideInLeft 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.08) 0.5s backwards;
}


请吸收上述设计语言里的光影、厚度和物理运动理念，接下来请帮我编写：
```

