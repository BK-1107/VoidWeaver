<div align="center">
  <h1>Void Weaver</h1>
  <p><b>把图像拆成可编辑的创作结构，再编织出新的视觉世界。</b></p>
  <a href="../LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/frontend-React%2018-61dafb?style=flat-square" alt="React">
  <img src="https://img.shields.io/badge/backend-Spring%20Boot-6db33f?style=flat-square" alt="Spring Boot">
  <img src="https://img.shields.io/badge/API-Gemini%20%2B%20NovelAI-8b5cf6?style=flat-square" alt="AI Engines">
</div>
<br/>

> Rewrite the World Protocol Active

[English](README_EN.md) | [日本語](../README.md)

<div align="center">
  <img src="assets/Snipaste_2026-06-17_00-42-28.png" width="1000" alt="Gemini Hackathon Google DeepMind">
  <p><b>Gemini Hackathon 参赛作品</b></p>
</div>

<br/>

<div align="center">
  <img src="https://img.youtube.com/vi/aGwaFVipMss/maxresdefault.jpg" width="1000" alt="Void Weaver 演示视频">
  <p><b>主页展示</b></p>
</div>


## Why

AI 生图工具越来越多，但大多数工具仍然把创作过程压缩成一段 prompt：你输入文字，模型输出图片，中间的结构很难被看见，也很难被稳定控制。

Void Weaver 想解决的是另一个问题：**怎样把一张参考图变成可以编辑、锁定、加权和迭代的创作结构。**

它会先读取参考图，把视觉信息拆解为风格、主体、姿态、服装、背景、构图、氛围等模块。用户可以像整理图层一样编辑这些模块：加强某个标签，删除不需要的描述，锁定人物姿态，只改背景，或者用自然语言告诉 AI 下一步要怎么变。

所以 Void Weaver 不是一个“输入 prompt 然后等待结果”的单向工具。它更像一个 AI 图像创作控制台：先解析现实，再重写现实。

## 使用方式

### 1. 配置生成环境

在左侧设置栏填写 Gemini API Key，并选择生成引擎。NovelAI 适合二次元和风格化生成，Google Imagen 更适合写实与综合创意生成。

### 2. 上传图像

把图片拖入 Source Material 区域。它会成为后续解析、图生图和风格提取的基础。

### 3. 解析图像

点击 DECIPHER，系统会调用 Gemini 分析画面，并生成一组结构化模块，例如服装、背景、动作等。解析结果支持继续微调。

<div align="center">
  <img src="assets/Snipaste_2026-06-17_00-05-32.png" width="900" alt="图像解析示例">
</div>

### 4. 编辑模块

你可以对解析出的模块继续调整：

- 删除不需要的标签
- 增强或削弱标签权重
- 锁定不想改变的模块
- 手动补充新的视觉描述

### 5. 图生图

在底部输入自然语言指令，例如：

```text
把衣服改成红色毛衣，表情双眼紧闭如同睡着了，斜45度半身照
```

Void Weaver 会根据锁定状态，只更新允许修改的模块。

点击 MANIFEST，系统会把当前模块组装成最终 prompt，并调用选定引擎生成新图。

<div align="center">
  <img src="assets/Snipaste_2026-06-17_00-17-00.png" width="900" alt="图生图示例">
</div>

### 6. 直接生成图

除了图生图，你还可以混合多图，或者根据自己的构想直接生成图像。生成前可以自定义画布大小、生成步数、模型类型等参数。

<div align="center">
  <img src="assets/Snipaste_2026-06-17_00-21-10.png" width="900" alt="直接生成图示例">
</div>

### 7. Deep Thinking

Deep Thinking 会让生成过程从结构草图开始，并对每一步进行视觉审查，让最终输出更稳定、更美观，同时整个过程可见。

<div align="center">
  <img src="assets/Snipaste_2026-06-17_00-18-50.png" width="900" alt="Deep Thinking 示例">
</div>

## 工作流

```text
Source Image
  -> Decipher
  -> Prompt Modules
  -> Lock / Weight / Refine
  -> Manifest
  -> New World
```

## 功能

| 功能 | 使用场景 | 它做什么 |
| :--- | :--- | :--- |
| 图像解析 | 拿到一张参考图，想提取其中的视觉结构 | 使用 Gemini 将图像拆解成多个可编辑模块 |
| 模块化 Prompt | prompt 太长、太乱、难以维护 | 把 prompt 拆成 Style、Subject、Pose、Costume、Background 等模块 |
| 标签权重 | 想让某些视觉元素更强或更弱 | 为单个标签设置权重，影响最终生成倾向 |
| 模块锁定 | 只想改局部，不想破坏主体 | 锁定指定模块，只让 AI 修改未锁定部分 |
| 自然语言精炼 | 想用一句话调整画面 | 输入修改指令，让 AI 重写相关模块 |
| 双引擎生成 | 需要不同风格的生成能力 | 支持 NovelAI 和 Google Imagen 两种路线 |
| Deep Thinking | 希望生成前有更强的自检过程 | 生成草图、执行视觉审查、输出修正指令，再生成最终图 |
| 历史与回放 | 想比较不同生成结果 | 保留生成历史，并查看 Deep Thinking 日志 |

## 技术设计

Void Weaver 使用前后端分离架构：

| 层 | 技术 | 说明 |
| :--- | :--- | :--- |
| 前端 | React 18 / TypeScript / Vite | 构建交互式创作工作台 |
| 状态管理 | Zustand | 管理图片、模块、生成历史和 UI 状态 |
| 样式 | TailwindCSS | 构建深色、模块化、控制台式界面 |
| 后端 | Spring Boot 3.2.1 | 提供图像解析、精炼和生成 API |
| AI 解析 | Gemini | 将图像转为结构化模块 |
| AI 生成 | NovelAI / Google Imagen | 根据最终 prompt 生成图像 |

## 环境要求

- Java 17+
- Node.js 18+
- Maven 3.8+
- Gemini API Key
- NovelAI API Token，可选
- Google Cloud Credentials，可选

## License

MIT License. Feel free to use, modify, and build on Void Weaver.
