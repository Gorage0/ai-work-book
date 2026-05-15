# 《AI工作场景落地实战》— 开发维护手册

> 本文档供 Codex 开发时参考，涵盖项目结构、设计规范、更新流程和部署方式。

---

## 一、项目概览

| 项目 | 说明 |
|------|------|
| 书名 | 《AI工作场景落地实战》 |
| 副标题 | 从第一个 Prompt 到搭建自己的 AI 系统 |
| 定位 | 写给白领的 AI 能力建设方法论，非技术向 |
| 线上地址 | https://ai-work-book.pages.dev/ |
| GitHub 仓库 | https://github.com/Gorage0/ai-work-book |
| 本地目录 | `D:\condex\AI剪辑\preview\` |
| 部署方式 | Cloudflare Pages，连接 GitHub main 分支，自动部署 |

---

## 二、文件结构（共24个HTML文件）

```
preview/
├── index.html                    # 全书目录导航页（入口）
├── 00-cover.html                 # 书籍封面
├── 00-preface.html               # 前言
│
├── chapter1-complete-v1.html     # 第1章：为什么这次AI离普通人这么近
├── chapter2-ai-history-v1.html   # 第2章：AI的前世今生
├── chapter3-transformer-v1.html  # 第3章：为什么Transformer是分水岭
├── chapter4-frontier-v1.html     # 第4章：今天前沿研究在卷什么
├── chapter5-vendors-v1.html      # 第5章：大模型厂商分别在做什么
├── chapter6-four-layers-v2.html  # 第6章：Prompt/Skill/Workflow/Agent四层递进
├── chapter7-20tasks-v1.html      # 第7章：AI最先能帮你做的20件白领工作
├── chapter8-office-skill-v1.html # 第8章：办公场景Skill实战
├── chapter9-data-modeling-v1.html# 第9章：数据建模与分析
├── chapter10a-html-intro-v1.html # 第10章A：HTML工具入门
├── chapter10b-html-product-v1.html # 第10章B：HTML产品化
├── chapter10c-html-maintain-v1.html # 第10章C：HTML维护
├── chapter11-workflow-audit-v1.html # 第11章：工作流审计
├── chapter12-skill-library-v1.html  # 第12章：Skill库建设
├── chapter13-workflow-build-v1.html # 第13章：工作流搭建
├── chapter14-agent-v1.html       # 第14章：搭建第一个Agent助手
├── chapter15-team-collab-v1.html # 第15章：团队协作与AI
├── chapter16-future-v1.html      # 第16章：未来展望
│
├── appendix-a-prompt-guide.html  # 附录A：Prompt工程核心技巧（10个）
├── appendix-b-skill-template.html # 附录B：Skill卡片模板与规范
└── appendix-c-tools.html         # 附录C：AI工具场景索引

CLAUDE.md                         # 本文档
```

### 章节分组

| 分组 | 章节 | 颜色主题 |
|------|------|----------|
| Part 1 认知基础 | Ch1–5 | 蓝色系（`#0f172a → #0c4a6e`） |
| Part 2 用起来 | Ch6–11 | 绿色系（`#052e16 → #166534`） |
| Part 3 建立AI系统 | Ch12–16 | 各章独立色（紫/橙/橙红/靛/蓝） |

---

## 三、设计规范

### 3.1 全局 CSS 变量

每个章节 HTML 文件头部都应包含以下 CSS 变量：

```css
:root {
  --primary: #2563eb;
  --primary-soft: #dbeafe;
  --accent: #f43f5e;
  --accent-soft: #ffe4e6;
  --ink: #0f172a;
  --ink-mid: #334155;
  --ink-soft: #64748b;
  --surface: #f1f5f9;
  --card: #ffffff;
  --border: rgba(15,23,42,.07);
  --orange: #f97316;
  --orange-soft: #ffedd5;
  --green: #16a34a;
  --green-soft: #dcfce7;
  --purple: #7c3aed;
  --purple-soft: #ede9fe;
  --teal: #0891b2;
  --teal-soft: #cffafe;
}
```

### 3.2 章节头部（chapter-header）

每章必须有一个深色渐变头部，结构如下：

```html
<div class="chapter-header">
  <!-- 两个伪元素光晕已在CSS里定义 -->
  <p class="ch-eyebrow">Chapter XX · Part X</p>
  <h1 class="ch-title">章节标题</h1>
  <p class="ch-subtitle">副标题说明</p>
  <div class="ch-takeaway">
    <strong>核心要点：</strong>一句话总结本章收获
  </div>
</div>
```

各 Part 头部渐变色：

| Part | 渐变 |
|------|------|
| Part 1 | `linear-gradient(135deg, #0f172a 0%, #0c4a6e 45%, #1e1b4b 100%)` |
| Part 2 | `linear-gradient(135deg, #052e16 0%, #166534 45%, #14532d 100%)` |
| Part 3 Ch12 | `linear-gradient(135deg, #1e1b4b 0%, #312e81 45%, #1e1b4b 100%)` |
| Part 3 Ch13 | `linear-gradient(135deg, #052e16 0%, #065f46 45%, #064e3b 100%)` |
| Part 3 Ch14 | `linear-gradient(135deg, #431407 0%, #9a3412 45%, #c2410c 100%)` |
| Part 3 Ch15 | `linear-gradient(135deg, #1e1b4b 0%, #3730a3 45%, #1e3a8a 100%)` |
| Part 3 Ch16 | `linear-gradient(135deg, #0f172a 0%, #1e3a8a 45%, #0f172a 100%)` |

### 3.3 核心内容组件

#### 卡片（.card）
```html
<div class="card">
  <div class="section-label">Section 01</div>
  <div class="section-title">小节标题</div>
  <div class="section-pill pill-blue">标签</div>
  <p class="body-text">正文段落...</p>
</div>
```

#### 标签色彩
```
pill-blue    → 蓝色
pill-green   → 绿色
pill-orange  → 橙色
pill-purple  → 紫色
pill-teal    → 青色
pill-red     → 红色
pill-gold    → 金色
pill-emerald → 翠绿
```

#### 特殊内容框

```html
<!-- 示例/案例框（橙色） -->
<div class="example-box">
  <p class="example-label">📋 真实案例</p>
  <p>内容...</p>
</div>

<!-- 洞见框（青色） -->
<div class="insight-box">
  <div class="ins-label">💡 关键洞见</div>
  <p>内容...</p>
</div>

<!-- 警告框（橙色边） -->
<div class="warn-box">内容...</div>

<!-- 代码块 -->
<div class="code-block-wrap">
  <div class="code-header">
    <div class="ch-dot" style="background:#ef4444;"></div>
    <div class="ch-dot" style="background:#f59e0b;"></div>
    <div class="ch-dot" style="background:#22c55e;"></div>
    <div class="ch-filename">文件名.md</div>
    <div class="ch-lang">MARKDOWN</div>
  </div>
  <div class="code-block">代码内容</div>
</div>
```

### 3.4 内容风格要求（重要）

- **禁止使用 bullet list（`<ul><li>`）写正文**，用叙事段落（`<p class="body-text">`）代替
- SVG 图表优先，用于展示流程、对比、层级关系
- 每章正文字数约 3000–5000 字
- 语气：口语化、直接、像和朋友聊天，不用"首先其次最后"等套话

---

## 四、页面模板

### 新建章节的最小模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>第X章 章节标题</title>
<style>
/* 复制任意一章的完整CSS粘贴到这里，修改 --primary 颜色即可 */
</style>
</head>
<body>
<div class="page">

  <div class="chapter-header">
    <p class="ch-eyebrow">Chapter XX · Part X</p>
    <h1 class="ch-title">标题</h1>
    <p class="ch-subtitle">副标题</p>
    <div class="ch-takeaway"><strong>核心要点：</strong>...</div>
  </div>

  <!-- 正文卡片 -->
  <div class="card">
    <div class="section-label">Section 01</div>
    <div class="section-title">小节标题</div>
    <p class="body-text">正文...</p>
  </div>

  <!-- 底部导航 -->
  <div class="page-nav">
    <a class="nav-link" href="上一章.html">← 上一章</a>
    <a class="nav-link" href="index.html">目录</a>
    <a class="nav-link" href="下一章.html">下一章 →</a>
  </div>

</div>
</body>
</html>
```

---

## 五、更新与部署流程

### 5.1 修改已有内容

1. 直接编辑 `D:\condex\AI剪辑\preview\` 目录下对应的 HTML 文件
2. 执行以下命令推送：

```powershell
cd "D:\condex\AI剪辑\preview"
git add 修改的文件名.html
git commit -m "简短说明改了什么"
git push
```

3. Cloudflare Pages 检测到 push 后约 **1分钟内**自动更新线上网站，无需任何手动操作。

### 5.2 新增章节或页面

1. 在 `preview/` 目录新建 HTML 文件
2. 在 `index.html` 的对应区域加入链接卡片
3. 推送：

```powershell
cd "D:\condex\AI剪辑\preview"
git add *.html
git commit -m "新增：XXX页面"
git push
```

### 5.3 批量推送所有改动

```powershell
cd "D:\condex\AI剪辑\preview"
git add *.html
git commit -m "更新说明"
git push
```

### 5.4 查看推送状态

```powershell
cd "D:\condex\AI剪辑\preview"
git log --oneline -5    # 查看最近5次提交
git status              # 查看哪些文件有改动未提交
```

---

## 六、index.html 维护说明

`index.html` 是全书入口，修改时注意：

### 添加新章节卡片

在对应 Part 的 `<div class="chapters-grid">` 里添加：

```html
<a class="ch-card p1" href="chapterX-xxx-v1.html">
  <div class="ch-num">第 X 章</div>
  <div class="ch-title-main">章节标题</div>
  <div class="ch-desc">一句话描述</div>
  <div class="ch-tag tag-1">标签</div>
</a>
```

颜色类：`p1`（蓝）、`p2`（绿）、`p3-12`至`p3-16`（各自颜色）

### 添加附录卡片

在 `<div class="appendix-grid">` 里添加：

```html
<a class="app-card" href="appendix-x-xxx.html">
  <div class="app-icon">📎</div>
  <div class="app-title">附录 X · 标题</div>
  <div class="app-desc">描述</div>
</a>
```

---

## 七、已知注意事项

### Ch14 SKILL.md 字段说明
- `name` 和 `description` 是 agentskills.io **官方必填字段**
- `effort`、`model`、`context: fork` 是 **Claude Code 等工具的扩展字段**，不是官方规范
- 描述时措辞用"工具生态在官方基础上扩展了这些字段"，不要说"规范定义了这些字段"

### Ch10 分三节
第10章拆成了10a/10b/10c三个文件，index.html 里用特殊的全宽卡片+子网格展示，修改时注意同步更新三个文件。

### 文件命名规则
- 章节文件：`chapter{N}-{slug}-v{版本}.html`
- 如有重大改版，新建 v2 文件并更新 index.html 链接，保留旧文件直到确认不再需要

---

## 八、线上访问地址汇总

| 页面 | 地址 |
|------|------|
| 目录首页 | https://ai-work-book.pages.dev/ |
| 封面 | https://ai-work-book.pages.dev/00-cover.html |
| 前言 | https://ai-work-book.pages.dev/00-preface.html |
| 第1章 | https://ai-work-book.pages.dev/chapter1-complete-v1.html |
| 附录A | https://ai-work-book.pages.dev/appendix-a-prompt-guide.html |
| 附录B | https://ai-work-book.pages.dev/appendix-b-skill-template.html |
| 附录C | https://ai-work-book.pages.dev/appendix-c-tools.html |

---

*最后更新：2026-05-16*
