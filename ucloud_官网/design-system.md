# ucloud官网 网页设计规范

> 本文档定义了 ucloud官网的网页设计规范。AI 代理在生成网页时应严格遵循以下规范，确保设计一致性。

---

## 一、颜色系统 (Color System)

> 本章节基于 UCLOUD UED 最新设计语言构建。
> 💡 [AI Agent 核心铁律]：严禁在 CSS 中硬编码具体的 HEX 色值。生成代码时必须 100% 映射到以下定义的 `var(--xxx)` Token。

### 1.1 品牌主色与辅助色 (Brand & Auxiliary)

| 颜色分类 | Token | Hex 值 / CSS 属性 | 用途说明 |
|---|---|---|---|
| **基本主色** | `--color-primary` | `#3860F4` | 全局主视觉、核心操作按钮、选中状态 (Active)、重要链接。 |
| **主渐变色** | `--gradient-primary` | `linear-gradient(90deg, #3860F4 0%, #4E8CFF 50%, #B5E6FF 100%)` | 核心主视觉背景、重点强调区块、大型主按钮底色。 |
| **辅助色(深)** | `--color-aux-dark` | `#2A315F` | 辅助深色背景、深色区块强调、深色页脚 (Footer)。 |

### 1.2 文本颜色系统 (Typography Colors)

AI 在生成文本代码时，必须优先使用以下专属 Token，以确保对比度和信息主次。

| 视觉层级 | Token (语义变量名) | Hex 值 | 用途及 HTML 标签映射 |
|---|---|---|---|
| **标题文本** | `--text-title` | `#1D273F` | 页面大标题、模块主标题。*(常用于 `<h1>`-`<h6>`, `<th>`, `<strong>`)* |
| **正文文本** | `--text-body` | `#50627F` | 常规段落正文、列表常规内容。*(常用于 `<p>`, `<td>`, `<span>`, `<li>`)* |
| **备注文本** | `--text-remark` | `#C3CAD9` | 次要辅助说明、表单占位符 (Placeholder)、表单提示语。 |
| **禁用文本** | `--text-disabled`| `#BBBBBB` | 不可点击的文字、禁用的输入框内容 *(常伴随 `.is-disabled` 类)*。 |

#### 💡[AI Agent 识别与生成规则]：文本层级分离约束
在一个完整的业务卡片或模块内，如果同时存在标题和正文，**AI 必须分开调用变量**。标题强制调用 `--text-title`，其下方描述性正文必须降级调用 `--text-body`。**绝对禁止**图省事在父容器上统一写死一种文字颜色。

### 1.3 页面背景与卡片底色 (Background & Surfaces)

| 容器层级 | Token | Hex / Gradient 值 | 用途说明 |
|---|---|---|---|
| **页面分割背景** | `--bg-page` | `#F6F8FD` | 页面最底层大背景 (Level 0)，用于区分不同的独立业务模块。 |
| **标准卡片底色** | `--bg-surface` | `#FFFFFF` | 标准卡片、弹窗的纯白底色（规范隐含，用于在页面背景上凸显层级）。 |
| **产品价格卡片** | `--bg-card-price`| `linear-gradient(180deg, #ECF0FF 0%, #FFFFFF 100%)` | 特殊高亮卡片背景（如 Pricing Tables, 特性聚焦卡片），带有从浅蓝到白的渐变过渡。 |

#### 💡 [AI Agent 识别与生成规则]：Z轴视觉剥离 (Z-Index Contrast)
在构建页面布局结构时，遇到 `<section>` 或最外层 `<body>` 时，必须使用 `--bg-page` (`#F6F8FD`)。而在其内部生成的独立容器（如 `<div class="card">`），必须使用带有阴影的纯白底色或 `--bg-card-price` 渐变色，**严禁**容器内外的背景色混为一体。

### 1.4 描边色系统 (Border Colors)

| 描边层级 | Token | Hex 值 | 用途说明 |
|---|---|---|---|
| **浅色描边** | `--border-light` | `#ECEFF6` | 默认状态下的卡片边框、列表/表格内部分割线、次要界线。 |
| **深色描边** | `--border-dark` | `#DDE3F2` | 强调用途的边框、交互悬停态 (Hover) 边框、深色底托上的分割线。 |

### 1.5 扩展辅助渐变色 (Extended Gradients)

用于图标底色、数据可视化图表、标签 (Tags) 或轻量级装饰元素的丰富渐变。

| 渐变分类 | Token | CSS 渐变值 |
|---|---|---|
| **辅助渐变 A** | `--gradient-aux-a` | `linear-gradient(90deg, #1D89F2 0%, #9DD6FF 100%)` |
| **辅助渐变 B** | `--gradient-aux-b` | `linear-gradient(90deg, #4C70F5 0%, #9DBBFF 100%)` |
| **辅助渐变 C** | `--gradient-aux-c` | `linear-gradient(90deg, #1DBEF2 0%, #9DE2FF 100%)` |

————

## 二、字体系统

### 2.1 字体族

```css
font-family: "PingFang SC", "Hiragino Sans GB", "微软雅黑", "Microsoft Yahei", tahoma, arial, "宋体", sans-serif;
```

### 2.2 字重规范定义 (Font Weights)

| 规范命名 | Token 变量名 | CSS数值 | 适用场景说明 |
|---|---|---|---|
| **常规** | `--font-weight-regular` | `400` | 副标题、正文、辅助说明、链接等大段阅读性文本。 |
| **中黑体** | `--font-weight-medium` | `500` | 一级至三级（20px）标题，用于提供适度的视觉强调而不显沉重。 |
| **中粗体** | `--font-weight-semibold`| `600` | 特别用于三级（18px）标题，在较小字号下保证标题的层级凸显。 |

### 2.3 核心排版阶梯 (Typography Scale & Line Height)

AI 在分析和生成具体的文本标签（如 `h1`-`h6`, `p`, `a`）时，必须直接提取以下成组的数值。为了绝对精准还原设计稿，建议 `line-height` 直接输出对应的像素值（或转化为精确的小数倍率）。

| 层级命名 | 字号 (Font Size) | 行高 (Line Height) | 字重 (Weight) / Token | 默认搭配的颜色 Token | 适用语义标签 |
|---|---|---|---|---|---|
| **一级标题** | `36px` | `54px` | 中黑体 `500` | `--text-title` | 页面最核心大标题 `<h1>` |
| **二级标题** | `24px` | `36px` | 中黑体 `500` | `--text-title` | 模块主标题 `<h2>` |
| **三级标题(大)**| `20px` | `32px` | 中黑体 `500` | `--text-title` | 卡片标题、次级模块标题 `<h3>` |
| **三级标题(小)**| `18px` | `28px` | 中粗体 `600` *(注意这里变粗了)* | `--text-title` | 小卡片标题、表单区块头 `<h4>` |
| **副标题** | `16px` | `25px` | 常规 `400` | `--text-title` / `--text-body` | 标题下方的导语、大号正文 |
| **链接文字** | `16px` | `25px` | 常规 `400` | 🔗强制关联 `--color-primary` | 超链接 `<a>`、文字按钮 |
| **正文(默认)** | `14px` | `25px` | 常规 `400` | `--text-body` | 全局默认阅读文本 `<p>`, `<td>`, `<li>` |
| **辅助文字** | `12px` | `24px` | 常规 `400` | `--text-remark` | 页脚声明、表单提示语、时间戳 |

#### 💡 [AI Agent 识别与生成规则]：排版组合三维检验 (Typography Composition)

当 AI 被要求生成一个具体的模块（例如：一个带有标题、正文和链接的卡片）时，必须在其内部执行以下组合校验逻辑：

1. **绝对组合绑定 (Strict Pairing):**
   - 只要使用 `14px` (正文)，行高必须写死为 `25px`，字重必须为 `400`。
   - 只要使用 `18px` (三级标题)，行高必须为 `28px`，且字重必须强制切为 `600`。
   - **防错预警：** 严禁出现如 `font-size: 14px; line-height: 1.5;`（这会导致 21px 行高，与设计稿 25px 不符）这种模糊计算代码。

2. **交互语义强制变色 (Affordance Override):**
   - 如果一段 `16px` 或 `14px` 的常规文本被赋予了点击事件（如 `<a href="#">了解更多</a>`），其颜色**禁止**继承父级的灰色。AI 必须为其单独声明 `color: var(--color-primary);` (`#3860F4`)，并且在 `:hover` 状态下增加下划线或透明度变化以完善无障碍交互。

3. **视觉降维原则 (Visual Downgrade):**
   - 在同一个列表或卡片内，标题使用了 `--text-title` (深黑 `1D273F`) 之后，下方的辅助文本必须主动识别并降级使用 `12px` 搭配 `--text-remark` (`#C3CAD9`)，以构建足够的纵深对比度。


---

## 三、 段落排版与间距系统 (Paragraph Layout & Spacing System)

> 本系统基于 UCLOUD UED 最新设计语言构建。
> 💡[AI Agent 核心铁律]：AI 在生成常规业务区块（如产品介绍、特性列表）时，必须严格遵守以下对齐原则与像素级间距组合，**严禁随意使用 `margin` 推挤**。

### 3.1 全局对齐原则 (Alignment Directives)

- **万物默认左对齐 (Default Left-Aligned):** 在没有任何特殊说明的情况下，所有的标题、正文、按钮、图文组合必须强制生成为左对齐（`text-align: left` 或 `align-items: flex-start`）。
- **无指令不居中 (No Auto-Centering):** 绝对禁止 AI 擅自根据业务上下文（如遇到 Hero 大屏幕区域）自动将内容居中。**必须且只有**在明确接收到“居中对齐”的特殊指令时，才能调用 `text-align: center`、`align-items: center` 及相关的居中排版结构。

### 3.2 段落内部垂直间距 (Vertical Spacing Logic)

在一个完整的文本段落块中，元素从上到下的间距必须遵循以下固定像素映射：

| 间距位置 (From -> To) | 规定间距值 | Token 建议 | 场景说明 / AI 生成约束 |
|---|---|---|---|
| **标题 -> 正文** | `8px` | `--spacing-sm` | 无论是 H1 还是 H3，只要下方紧跟正文或辅助文字，`margin-bottom` 或 `gap` 必须固定为 `8px`。 |
| **正文 -> 文字链接** | `24px` | `--spacing-lg` | 正文段落结束，下方出现“了解详情 ->”等纯文字链接时，垂直间距为 `24px`。 |
| **正文 -> 独立按钮** | `32px` | `--spacing-xl` | 正文段落结束，下方出现独立的纯色大按钮（如 48px 高的主操作按钮），垂直间距为 `32px`。 |
| **大图标 -> 标题** | `24px` | `--spacing-lg` | 当图标大小大于等于68px，采用“上下排版”或“左右排版”时，大图标距离下方、右方标题的间距必须为 `24px`。 |
| **小图标 -> 标题** | `12px` | `--spacing-md` | 当图标大小小于68px，采用“左右排版”时，小图标距离右方标题的间距必须为 `12px`。 |

### 3.3 图文组合水平间距 (Horizontal Spacing Logic)

| 间距位置 (From -> To) | 规定间距值 | Token 建议 | 场景说明 / AI 生成约束 |
|---|---|---|---|
| **文字链接 -> 箭头图标** | `6px` | `--spacing-xs` | “了解详情 ->” 这类带箭头的可点击文字链，文字与右侧箭头的间距为 `6px`。 |

### 3.4 块级组合间距 (Block Inter-spacing)

| 间距位置 | 规定间距值 | 场景说明 / AI 生成约束 |
|---|---|---|
| **段落块 -> 下一个段落块** | `32px` | 常用于列表中（如案例一中的 3级标题段落之间），每个独立项的垂直间距。 |

---

### 3.5 💡 [AI Agent 识别与生成规则]：典型段落结构代码范式

AI 遇到图文段落生成需求时，必须采用 **Flexbox + Gap** 的现代 CSS 布局方式，以精准控制上面定义的间距，严禁在子元素上滥用 `margin`。

**✅ 范例 A：带文本链接的常规左对齐段落**
```html
<div class="paragraph-block">
  <h2 class="title-h2">2级标题</h2>
  <p class="body-text">在全球30多个可用区上线云主机产品，为您提供高可用的服务方案。</p>
  <a href="#" class="text-link">了解详情 <i class="icon-arrow"></i></a>
</div>

<style>
/* AI 必须按此规则输出 CSS */
.paragraph-block {
  display: flex;
  flex-direction: column;
  align-items: flex-start; /* 强制左对齐 */
  /* 不要在这里统一下发 gap，因为内部间距不同 */
}
.paragraph-block .title-h2 {
  margin-bottom: 8px; /* 标题到正文: 8px */
}
.paragraph-block .body-text {
  margin-bottom: 24px; /* 正文到文字链: 24px */
}
.paragraph-block .text-link {
  display: inline-flex;
  align-items: center;
  gap: 6px; /* 文字到右侧箭头: 6px */
  color: var(--color-primary); /* 必须调用品牌主色 */
  font-size: 16px;
}
</style>
```

### 4.1 通栏背景与中心内容区 (Full-Bleed Background & Center Container)

> 💡[大屏适配防错铁律]：绝对禁止在最外层容器（如 body, wrapper, banner）上硬编码 `width: 1920px;`。必须采用“通栏背景 + 居中定宽内容区”的经典架构，以完美适配超大屏幕（2K/4K）。

| 容器层级 | CSS 核心逻辑与设定 | 约束说明与防错指南 |
|---|---|---|
| **第一层：通栏背景层 (Full-Width Wrapper)** | `width: 100%;` <br>`min-width: 1280px;` | 用于承载置顶行底色、Banner 背景大图、深色区块的底板。使用 `100%` 确保在大于 1920px 的大屏上背景能无限向左右延伸。如果包含背景图，必须搭配 `background-size: cover; background-position: center;` 以防截断。 |
| **第二层：中心内容区 (Container)**| `width: 1440px;`<br>`margin: 0 auto;`<br>`padding: 0 36px;` | **所有的**文字、图片、网格卡片等实体内容，必须被强制包裹在此第二层容器内。这保证了在超大屏幕上，用户的视线不需要左右来回大范围移动，内容始终居中展示。 |

**✅ AI 容器生成标准代码范式：**
```css
/* 外层容器：负责背景色的无限延伸 (如 Banner 区域) */
.section-full-wrapper {
  width: 100%;           /* 确保大屏背景拉通 */
  min-width: 1280px;     /* 兜底最小宽度，防挤压 */
  background: url('banner-bg.jpg') center/cover no-repeat; /* 居中裁剪式延伸 */
}

/* 内层容器：负责真实内容的固定与安全边距 */
.ucloud-container {
  width: 1440px;         /* 锁定内容区最大宽度 */
  margin: 0 auto;        /* 保证在 100% 的父级中绝对居中 */
  padding: 0 36px;       /* 强制左右安全距离 */
  box-sizing: border-box;
}
```
### 4.2 响应式断点与自适应系统 (Breakpoints & Responsive Layout)

> 💡[AI Agent 核心铁律]：AI 在生成代码时，默认优先输出基于 PC 端大屏（1920px）的样式，但**必须**同时包含以下 `@media` 查询代码，实现从 PC 到移动端的优雅降级（Graceful Degradation）。严禁省略响应式代码。

#### 4.2.1 核心视口与容器映射表 (Viewport to Container Mapping)

基于 UCLOUD UED 规范，内容容器在不同屏幕宽度下必须严格对应以下尺寸和安全边距：

| 屏幕类型 | 触发断点 (Media Query) | 中心内容区宽度 (Container Width) | 左右安全边距 / 留白 | 网格等分系统 (Grid) |
|---|---|---|---|---|
| **超大桌面 (2K+)** | `>= 1920px` | 强制 `1440px` | 内部 Padding `36px` | 2 / 3 / 4 等分 |
| **标准桌面 (Desktop)** | `>= 1440px` 且 `< 1920px` | 强制 `1200px` | 外部留白至少 `60px` | 2 / 3 / 4 等分 |
| **小桌面/横屏平板** | `>= 1024px` 且 `< 1440px` | 强制 `904px` | 外部留白至少 `60px` | 2 / 3 等分 |
| **平板 (Tablet)** | `>= 768px` 且 `< 1024px`| 强制 `648px` | 外部留白至少 `60px` | 降级为 2 等分 |
| **移动端 (Mobile)** | `< 768px` (基准 375px) | 随屏幕自适应 `100%` | 强制 Padding `22px` | 降级为 1 列 (单列铺满) |

#### 4.2.2 响应式卡片阵列重排逻辑 (Grid Reflow Engine)

当设计稿出现并排的业务卡片（如“4等分”产品优势、“3等分”解决方案）时，AI 必须使用 `CSS Grid` 并按照以下逻辑编写断点，绝对禁止卡片在小屏幕上被暴力挤压变形。

**等分降级公式：**
- **4等分阵列：** PC (`4列`) -> 小桌面 (`2列`) -> 平板 (`2列`) -> 移动端 (`1列`)。
- **3等分阵列：** PC (`3列`) -> 小桌面 (`3列`) -> 平板 (`1列` 或横向滚动) -> 移动端 (`1列`)。

#### 4.2.3 💡[AI Agent 识别与生成规则]：标准自适应 CSS 代码骨架

AI 在生成通用业务区块时，**必须直接套用以下 CSS 变量和响应式范式**构建 `.ucloud-container`，禁止随意发明断点。

```css
/* AI 必须生成的标准容器与响应式骨架 */
.ucloud-container {
  /* 1. 默认大屏形态 (优先 1920px 规范) */
  width: 1440px;
  margin: 0 auto;
  padding: 0 36px;
  box-sizing: border-box;
}

/* 2. 标准桌面降级 */
@media screen and (max-width: 1919px) {
  .ucloud-container {
    width: 1200px;
    padding: 0; /* 宽度已有余量，依靠 margin auto 留白 */
  }
}

/* 3. 小桌面降级 */
@media screen and (max-width: 1439px) {
  .ucloud-container {
    width: 904px;
  }
}

/* 4. 平板降级 */
@media screen and (max-width: 1023px) {
  .ucloud-container {
    width: 648px;
  }
}

/* 5. 移动端流式布局 */
@media screen and (max-width: 767px) {
  .ucloud-container {
    width: 100%;
    padding: 0 22px; /* 移动端左右 22px 安全边距 */
  }
}

/* 典型的 4列网格降级写法示例，AI 须以此为准 */
.grid-4-cols {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px; /* 标准间距 */
}
@media screen and (max-width: 1439px) {
  .grid-4-cols { grid-template-columns: repeat(2, 1fr); gap: 24px; }
}
@media screen and (max-width: 767px) {
  .grid-4-cols { grid-template-columns: 1fr; gap: 16px; }
}
```

---

## 五、 基础视觉变量系统 (Foundational Visual Tokens)

除了颜色和字体，AI 在构建页面容器时，必须严格调用以下圆角和阴影 Token，严禁随意编造 px 数值。

### 5.1 圆角系统 (Border Radius) 与嵌套约束

| Token 变量 | 尺寸 (px) | 适用场景 |
|---|---|---|
| `--radius-sm` | `4px` | 极小元素：Tag 标签、Checkbox、Tooltip。 |
| `--radius-md` | `8px` | 中小元素：、Input 输入框、内部小图表。 |
| `--radius-lg` | `12px` | 次级容器：卡片内部的嵌套底板、小模块。 |
| `--radius-xl` | `16px` | **(默认全局圆角)** 主卡片、弹窗 (Modal)、大型业务容器。 |
| `--radius-2xl`| `24px` | 特殊大型容器：Hero 区域的背景板、底部浮层。 |
| `--radius-full`| `9999px`| 胶囊按钮、圆形头像 (Avatar)。 |

#### 💡[AI Agent 识别与生成规则]：圆角默认值与同心嵌套法则 (Concentric Radius Rule)
1. **默认法则：** 当生成常规的业务卡片 (Card) 或内容容器时，**一律默认使用 `--radius-xl` (16px)**，除非有明确的特殊要求。
2. **嵌套同心法则 (Critical Geometry)：** 当出现“容器内嵌容器”（例如 16px 的大卡片里面，包着一个带有背景色的灰底小卡片或图片）时，为了视觉上的同心协调，**内部元素的圆角必须小于外部容器的圆角**。
   - **推导公式：** `内部圆角 ≈ 外部圆角 - 外部容器的 Padding`。
   - **执行指令：** 如果外层主卡片使用了 `--radius-xl` (16px)，其内部包裹的带背景子容器，**严禁**继续使用 16px，必须降级使用 `--radius-md` (8px) 或 `--radius-lg` (12px)。

---

### 5.2 阴影系统 (Shadows)

阴影用于体现元素的 Z 轴高度。请使用真实的 RGBA 投影，切勿使用纯黑或灰色硬边。

```css
/* 请 AI 直接应用以下 CSS 变量构建阴影 */
:root {
  --shadow-sm: 0 4px 4px -2px rgba(23, 25, 49, 0.04);  /* 常规边框替代、轻微凸起 */
  --shadow-md: 0 8px 20px 0px rgba(23, 25, 49, 0.08);   /* 常规卡片默认悬停态 */
}
```
---
## 六、 按钮系统 (Button System)

> 💡[AI Agent 核心铁律]：按钮必须严格遵循 `48px`（常规）或 `52px`（大型/强调）的高度标准。圆角统一锁定为 `10px`。AI 必须根据父容器背景色自动切换“浅色/深色模式”按钮样式。

### 6.1 按钮类型与视觉变量映射

| 按钮层级 | 状态 (State) | 背景 (Background) | 描边 (Border) | 文字颜色 (Text) | 适用场景 |
|---|---|---|---|---|---|
| **主按钮 (Primary)** | **默认** | `#3860F4` | 无 | `#FFFFFF` | 核心 CTA、主要操作 |
| | **悬停 (Hover)** | 渐变: `#08B0FD` - `#0B99FE` | 无 | `#FFFFFF` | 鼠标悬停时色彩增亮 |
| **次按钮 (Secondary)** | **默认** | `#FFFFFF` | `1px solid #E6EAF4` | `#1D273F` | 次要操作、白色底区块 |
| | **悬停 (Hover)** | `#FFFFFF` | `1px solid #3860F4` | `#3860F4` | 边框与文字同步变色 |
| **深色底按钮** | **默认** | `#FFFFFF` | `1px solid #E6EAF4` | `#1D273F` | 蓝色/深色背景上的反色按钮 |
| | **悬停 (Hover)** | `#FFFFFF` | `1px solid #C4CEF3` | `#3860F4` | 较浅的描边反馈 |
| **禁用态 (Disabled)** | **默认** | `#FFFFFF` | `1px solid #C8CDDA` | `#C8CDDA` | 不可点击状态 |

### 6.2 尺寸与间距规范 (Dimensions & Padding)

- **高度 (Height):** 默认为 `48px`。在 Hero Section 或需要极度强调的场景下使用 `52px`。
- **圆角 (Radius):** 强制固定为 `10px`。
- **文字大小 (FontSize):** 强制固定为 `16px`。
- **内边距 (Padding):**
  - **纯文字按钮:** 左右内边距固定为 `32px`。
  - **带箭头按钮:** 左右内边距固定为 `24px`，文字与右侧箭头的间距随 Hover 状态变化（见交互规则）。

### 6.3 文字链与箭头交互 (Link Buttons)

| 状态 | 文字颜色 | 箭头间距 (Gap) | 说明 |
|---|---|---|---|
| **默认** | `#1D273F` | `6px` | 经典的“了解详情 ->”结构 |
| **悬停 (Hover)** | `#3860F4` | `12px` | 箭头向右滑动，间距由 6px 增加至 12px |

---

### 6.4 💡 [AI Agent 识别与生成规则]：按钮 CSS 代码范式

AI 在生成按钮代码时，必须包含 `transition` 以确保平滑交互，并根据指令添加 `.has-arrow` 类。

**✅ 基础主按钮 CSS:**
```css
.btn-primary {
  height: 48px;
  padding: 0 32px;
  background-color: #3860F4;
  color: #FFFFFF;
  border-radius: 10px;
  border: none;
  font-size: 16px;
  font-weight: 500;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

```

## 七、AI Agent 全局核心铁律 (Global Directives)

当接收到用户的 UI 生成、代码转换或组件设计指令时，AI 必须在后台运行以下安全检查逻辑。任何违反以下原则的代码将被视为**生成失败**：

- **[规则 1] 绝对禁止硬编码 (No Hardcoding)**
  颜色、字号、圆角、阴影必须 100% 映射到本文档定义的 `var(--xxx)` Token 或指定的 Hex 值，严禁出现规范外的魔术数字（如 `#333`, `font-size: 15px`）。

- **[规则 2] 严格守住 1440px 红线 (Layout Bounds)**
  除带有通栏背景的 `Wrapper` 容器外，所有的文本、交互按钮、业务卡片、表格，绝对禁止突破 `1440px` 的最大宽度限制。

- **[规则 3] 字体三维解耦拼装 (Typography Decoupling)**
  禁止给 HTML 标签绑定死板的字体样式。必须将 `font-size` (尺寸)、`font-weight` (粗细)、`color` (文本专属颜色) 作为三个独立变量进行组合声明。

- **[规则 4] 无障碍与对比度红线 (Contrast Rule)**
  只要父级背景使用了品牌主色或品牌渐变色，其内部包裹的任何文本和图标必须强制切换为反白色。

## 八、版本历史

| 版本 | 日期 | 更新内容 |
|------|------|----------|
| 1.0 | 2026-05-11 | 初始版本，基于 ucloud 设计规范图片创建 |
