# SurferCloud 网页设计规范

> 本文档定义了 SurferCloud 品牌的网页设计规范。AI 代理在生成网页时应严格遵循以下规范，确保设计一致性。

---

## 一、颜色系统

### 1.1 中性色（Grey Scale）

| 色阶 | Token | Hex 值 | 用途 |
|------|-------|--------|------|
| Grey 1 | `--color-grey-1` | `#FBFBFF` | 浅色背景、一级卡片、主容器底色|
| Grey 2 | `--color-grey-2` | `#F6F8FF` | 二级卡片（卡片上的卡片）、选项组底托、表头背景 |
| Grey 3 | `--color-grey-3` | `#EBF0FC` | 三级容器、未选中状态的块状按钮/标签底色 |
| Grey 4 | `--color-grey-4` | `#D8DCEE` | 浅色边框、分割线 |
| Grey 5 | `--color-grey-5` | `#B5BACF` | 强调色|
| Grey 6 | `--color-grey-6` | `#787D91` | 深黑色背景取色4|
| Grey 7 | `--color-grey-7` | `#4C5064` | 深黑色背景取色3|
| Grey 8 | `--color-grey-8` | `#212633` | 深黑色背景取色2|
| Grey 8 | `--color-grey-9` | `#0D0A1A` | 深黑色背景取色1|
#### 💡 [AI Agent 识别与生成规则]：嵌套 UI 层级色彩判定 (Nested Cards Hierarchy)

在进行前端页面还原、UI 测试或代码生成时，如果遇到**“容器内嵌套容器”**（即卡片上的卡片）的结构，必须遵循“视觉层级（Z轴）递进原则”，以确保界面具有空间感。请 AI 严格按照以下逻辑识别和应用背景色：

1. **Level 0 (页面大背景):** 通常为纯白 `#FFFFFF`。
2. **Level 1 (主卡片 / 一级容器):** 例如最外层卡片的底色、大型表单的主容器。
   - **强制要求:** 背景色必须使用 `Grey 1 (#FBFBFF)`。
3. **Level 2 (次级卡片 / 嵌套底板):** 处于 Level 1 内部的次级包裹元素，例如：
   - 包含多选选项组的外层包裹底色。
   - 未处于选中状态的块状选
   - 数据列表的浅色表头 (Table Header)。
   - **强制要求:** 为了与一级背景形成对比，背景色 **禁止** 使用纯白或 Grey 1，必须向下取深一到两阶的颜色，即使用 `Grey 2 (#F6F8FF)` 或 `Grey 3 (#EBF0FC)`。

### 1.2 品牌色（蓝色系）

| 色阶 | Token | Hex 值 | 用途 |
|------|-------|--------|------|
| Blue 1 | `--color-blue-1` | `#F4F9FF` | 浅色一级 |
| Blue 2 | `--color-blue-2` | `#E6F1FF` | 浅色二级 一级灰色卡片上的跳转按钮色|
| Blue 3 | `--color-blue-3` | `#C3DFFF` | 浅色三级 |
| Blue 4 | `--color-blue-4` | `#8EC3FF` | 浅色四级 |
| Blue 5 | `--color-blue-5` | `#3D89FA` | 主色、强调色、链接颜色、数字颜色、简单icon颜色、选中状态的描边颜色|
| Blue 6 | `--color-blue-6` | `#165FCB` | - |
| Blue 7 | `--color-blue-7` | `#0645A1` | - |
| Blue 8 | `--color-blue-8` | `#002A68` | - |
| Blue 9 | `--color-blue-9` | `#00204E` | - |
|| Blue 10 | `--gradient-brand` | `linear-gradient(180deg, #8EC3FF 0%, #3D89FA 100%)` | 主按钮 (Primary CTA) 垂直渐变底色 |


### 1.3 [AI Agent 核心规则]：跨色系与组件组合约束 (Cross-Color Component Anatomy)

在复杂的业务容器中，经常会出现“品牌色导航 -> 中性色内容区 -> 品牌色次级操作”的嵌套解耦结构。为了保证视觉层级的主次分明，AI 在生成或分析此类组件时，必须遵循以下“视觉权重递减”规则：

**场景描述：选项卡 (Tabs) 与关联内容区 (Content Area) 的色彩搭配**


1. **内容承载层 (Content Container): 视觉降噪**
   - **约束:** 紧贴在活跃 Tab 下方的大型内容面板（如包含服务器配置表格的区域），**严禁**大面积延续使用品牌主色。
   - **选色:** 必须切换至**中性色系统 (Grey Scale)**，通常使用 Level 0 (`#FFFFFF`) 或 Level 1 (`--color-grey-1`) 作为大底板，以提供干净的阅读环境。

2. **内容区内部次级操作 (Secondary Actions inside Container): 建立弱引导**
   - **场景:** 在中性色的内容表格中，每一行可能有一个“跳转/购买”按钮（如 `->` 图标按钮）。
   - **约束:** 这些按钮如果使用实心主色（Blue Primary）会造成页面全是视觉焦点，显得杂乱。
   - **选色:** 必须使用 **--color-blue-2** 作为底板，搭配深色品牌色图标/文字。
   - **强执行标准:** 请提取表格内普通操作按钮的背景色，必须对应到 `--color-blue-2` (`#E6F1FF` ) ；其中的图标或文字颜色使用`--color-blue-5`(`#3D89FA` )以保证对比度。

**总结给 AI 的公式：**
`Tab Active (强蓝)` + `Content Box (中性白/灰)` + `Inner Normal Button (浅蓝底 Blue 2 + 深蓝字)` = **正确的视觉层级解耦**。

### 1.4 按钮 (Buttons)

按钮分为三个主要视觉层级，并包含明确的交互状态（Hover）。在生成 UI 代码时，请严格按照以下映射关系组合 Token。

| 按钮层级 / 命名 | 状态 (State) | 背景 (Background) | 文字颜色 (Text) | 边框 (Border) | 适用场景 (Usage) |
|-----------------|--------------|-------------------|-----------------|---------------|------------------|
| **主按钮 (Primary)** | **默认 (Default)** | 品牌蓝渐变 (`--gradient-brand`) | 纯白 `#FFFFFF` | 无 | 页面级核心操作 (CTA)，如“注册”、“提交”、“去支付”。一个区块内通常只出现一个主按钮。 |
| *(高视觉权重)* | **悬停 (Hover)** | 深色品牌渐变 `linear-gradient(180deg, #8EC3FF 0%, #3D89FA 100%)`| 纯白 `#FFFFFF` | 无 | 主按钮的鼠标悬停反馈，**注意：从渐变色突变为深色渐变**。 |
| **次按钮 (Secondary)**| **默认 (Default)** |纯白 `#FFFFFF`| `--color-blue-5` | `#D8DCEE`| 表格内操作、表单的“取消”、次级引导。用于视觉降噪。 |
| *(中视觉权重)* | **悬停 (Hover)** | `--color-blue-3`|  `--color-blue-5` | `#D8DCEE` | 次按钮的鼠标悬停反馈，背景色阶加深一层。 |
| **深色白底次按钮**| **默认 (Default)** | 纯白 `#FFFFFF`| `--color-blue-5`  | 无 | 深色背景上的反色操作 |
| *(中视觉权重)* | **悬停 (Hover)** | `--color-blue-3`| `--color-blue-5`  | 无 | 深色白底次按钮的悬停反馈 |

#### 💡[AI Agent 识别与生成规则]：按钮层级与状态约束 (Button Hierarchy & States)

1. **唯一性原则 (Primary CTA Rule):** 
   - 在识别或生成一个独立的表单、弹窗或主要营销区块时，**主按钮必须是唯一的**。如果遇到多个平行的操作，必须主动将其降级为“次按钮”。
   - 在深色底上，深色白底次按钮替换次按钮

2. **状态联动规则 (Hover State Engine):**
   - **AI 在编写 CSS 时必须包含 `:hover` 伪类。**
   - **降级逻辑：** 遇到次级按钮时，AI 需理解其 Hover 状态的本质是**“背景色阶加深 1 到 2 级”**。例如，Default 使用了 `--color-blue-1`，Hover 时必须切换为 `--color-blue-2`。

3. **跨色系组合验证 (Contextual Validation):**
   - 结合前文的“跨色系与组件组合约束”，如果按钮处于中性色（Grey Scale）的嵌套表格或卡片内，**严禁**大量使用“主按钮（渐变蓝）”。必须默认调用“次按钮（浅蓝底）”样式，以防止页面视觉焦点爆炸。

### 1.5 文本颜色系统 (Typography Colors)
文本颜色用于控制页面中所有字体的色彩层级。AI 在生成代码时，必须优先使用以下专属的文本 Token，以确保阅读的对比度、信息主次和交互指引。

| 视觉层级 | Token (语义变量名) | Hex 值 | 对应设计稿命名 | 适用场景及 HTML 标签映射 |
|---|---|---|---|---|
| **一级文字/标题** | `--text-title` | `#2E3A57` | 标题Grey1 | 页面大标题、模块主标题、重要数据展示。<br>*(常用于 `<h1>`-`<h6>`, `<th>`, `<strong>`)* |
| **二级文字/正文** | `--text-body` | `#616F8A` | 正文Grey2 | 常规段落正文、列表常规内容、表单已输入文字。<br>*(常用于 `<p>`, `<td>`, `<span>`, `<li>`)* |
| **三级文字/辅助** | `--text-remark` | `#C3CAD9` | 备注Grey3 | 次要辅助说明、表单占位符 (Placeholder)、时间戳。<br>*(常用于 `::placeholder`, 辅助描述文案)* |
| **禁用态文字** | `--text-disabled`| `#E1E6F0` | 禁用Disable | 不可点击的文字、禁用的输入框内容。<br>*(常伴随 `.is-disabled` 类或 `disabled` 属性)* |
| **反白/深色底文字**| `--text-inverse` | `#FFFFFF` | 标题White | 必须用于深色背景、品牌主色背景、渐变背景之上。<br>*(例如：主按钮内部文字)* |
| **🔗 链接/交互文字**| `--color-blue-5` | `#3D89FA` | (品牌蓝链接) | 纯文本链接、表格内的文字按钮、面包屑导航的可点项。<br>*(强制用于 `<a>` 标签及带有鼠标悬停交互的文字)* |

#### 💡[AI Agent 识别与生成规则]：文本层级与交互状态约束

1. **标题与正文的分离 (Hierarchy Mapping):**
   - 严禁全局使用同一种颜色。标题必须调用 `--text-title`，其下方的描述性正文必须降级调用 `--text-body`。
2. **输入框的动态变色 (Input Field States):**
   - 未输入前的提示词 (Placeholder) 必须使用 `--text-remark`；用户正在输入或已输入的内容，必须变深切换为 `--text-body`。
3. **强制无障碍对比度 (WCAG Contrast Rule):**
   - 如果父级容器的背景色使用了品牌深蓝或渐变色，其内部的文本**禁止**使用任何灰色系，**必须强制切换为反白色** `--text-inverse`。
4. **文字链接的交互识别 (Text Link Affordance):**
   - **绝对约束：** AI 在生成带有 `href` 属性的 `<a>` 标签，或纯文字形态的可点击按钮（如表格里的“Edit”、“Delete”）时，**禁止**继承父级的灰色正文颜色，**必须显式声明**颜色为品牌蓝 `--color-blue-5` (`#3D89FA`)。
   - **交互反馈 (Hover)：** 当鼠标悬停（`:hover`）在文字链接上时，没有hover颜色，只显示手型。
---

## 二、字体系统

### 2.1 字体族

```css
font-Satoshi-Regular, Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif
```

### 2.2 字号与行高

|### 2.2 排版与字体系统 (Typography System)

本系统采用**“字号与字重解耦 (Decoupled Size & Weight)”**的设计理念。AI 在生成样式时，必须将字号 Token、字重 Token、颜色 Token 独立组合使用。

#### 2.2.1 字号与行高 (Font Sizes & Line Heights)

共有 6 种标题级别字号，以及标准正文/辅助字号。行高 (Line Height) 采用无单位的相对倍数（如 1.5），以保证继承性和自适应。

| 级别 | Token (字号) | 尺寸 (Size) | 默认行高 (Line Height) | 用途与 HTML 语义映射 |
|------|--------------|-------------|------------------------|----------------------|
| **H1** | `--font-size-h1` | `52px` | `1.5` (78px) | 页面顶级大标题、Hero Section 标语 (`<h1>`) |
| **H2** | `--font-size-h2` | `48px` | `1.5` (72px) | 模块主标题、大型弹窗标题 (`<h2>`) |
| **H3** | `--font-size-h3` | `36px` | `1.5` (54px) | 次级模块标题、数据面板大数字 (`<h3>`) |
| **H4** | `--font-size-h4` | `24px` | `1.5` (36px) | 卡片标题、内容区块表头 (`<h4>`) |
| **H5** | `--font-size-h5` | `18px` | `2` (36px) | 小卡片标题、大正文引言 (`<h5>`, 强调正文) |
| **H6** | `--font-size-h6` | `16px` | `2` (32px) | 基础正文大小(`<h6>`) |

#### 2.2.2 字重规范 (Font Weights)

共有 5 种字重阶梯。AI 禁止直接写死具体的数值（如 `font-weight: 700`），必须使用对应的 Token 以保证全局一致性。

| 名称 | Token (字重) | CSS 数值 | 适用场景 |
|------|--------------|----------|----------|
| **常规体** | `--font-weight-regular` | `400` | 绝大多数正文、次要说明、默认表单输入文本 |
| **中黑体** | `--font-weight-medium` | `500` | 按钮文字、表格表头、悬停高亮文字、次要强调 |
| **半粗体** | `--font-weight-semibold`| `600` | 小标题、卡片次级标题、重要数据字段名 |
| **粗体** | `--font-weight-bold` | `700` | 主标题 (H1-H4)、重要强调信息 |
| **极粗体** | `--font-weight-black` | `900` | 特殊营销数字、超大字体的视觉强调焦点 |

---

#### 💡[AI Agent 识别与生成规则]：字体系统的拼装逻辑 (Typography Composition Rules)

在分析设计稿（如命名规则 `EN/h1-52px/grey1/black`）或编写 CSS 代码时，AI 必须遵循**“三维组合拼装法”**：

1. **分离变量法则 (Variable Separation):**
   - 绝对不要假设 `h1` 永远是粗体。
   - 当需要实现一个 `h1-52px/grey1/black` 的视觉效果时，AI 必须拆解并生成如下组合 CSS：
     ```css
     font-size: var(--font-size-h1);       /* 决定大小 52px */
     line-height: 1.5;                     /* 遵循 H1 行高设定 */
     font-weight: var(--font-weight-black);/* 决定字重 900 */
     color: var(--text-title);             /* 决定颜色，参照文本颜色规范 */
     ```

2. **降级与对比原则 (Typographic Hierarchy):**
   - 在同一个内容卡片内，如果标题使用了 `--font-weight-bold` (700) 加 `--text-title`，紧随其后的正文 **必须主动降级** 使用 `--font-weight-regular` (400) 加 `--text-body`。严禁在一个区块内铺满同一种高字重的文本。

3. **行高声明规范 (Line Height Syntax):**
   - AI 在编写 CSS 时，`line-height` **强烈建议使用无单位数值**（如 `1.5`），禁止使用带 `px` 或 `%` 的死值，以确保文字在多行折行时能根据 `font-size` 完美自适应缩放。


---

## 三、间距系统

### 3.1 基础间距单位

基础间距单位为 `4px`，所有间距应为 4 的倍数。

### 3.2 间距 Token

| Token | 值 | 用途 |
|-------|-----|------|
| `--spacing-xs` | 4px | 极小间距、图标与文字间距 |
| `--spacing-sm` | 8px | 小间距、紧凑布局 |
| `--spacing-md` | 16px | 默认边距、中等间距、元素内边距 |
| `--spacing-lg` | 24px | 大间距、卡片内边距 |
| `--spacing-xl` | 32px | 超大间距、区块间距 |
| `--spacing-2xl` | 48px | 极大间距、大区块间距 |
| `--spacing-3xl` | 64px | 页面级间距 |

### 3.3 大标题间距规范

| 场景 | 间距值 |
|------|--------|
| 每个大模块之间间距 | 60px |
| 每个大模块之间间距（紧凑） | 48px |
| 每个大模块之间间距（宽松） | 80px |
| 每个大模块之间间距（超宽） | 100px |
.**间距声明规范 :**
   - 默认情况下，网页端的大模块间距都是80px

---

## 四、布局系统 (Layout & Grid System)

本系统采用“通栏背景定宽居中”的宏观骨架，结合“移动端优先”的流式断点进行构建。AI 在生成页面级容器和模块排列时，必须严格遵守以下规范。

### 4.1 全局视口与中心内容区 (Viewport & Container)

| 容器层级 | 默认/最大宽度 | 核心特征与 CSS 逻辑 | 包含内容 |
|---|---|---|---|
| **页面视口 (Viewport)** | `100%` (基准 `1920px`) | `width: 100%;` | 仅用于承载贯穿全屏的背景色、背景渐变、底层装饰图案（如顶部深色 Hero 背景）。 |
| **中心内容区 (Container)**| `1200px` | `max-width: 1200px; margin: 0 auto;` | **所有的**文字标题、卡片、表格、栅格等实际业务内容，必须被强制约束在此容器内，禁止溢出拉伸。 |

### 4.2 响应式断点与栅格参数 (Breakpoints & Parameters)

| 屏幕类型 | 断点 (Media Query) | 左右安全边距 (Padding) | 列数 (Columns) | 槽宽 (Gutter) | 模块上下间距 (Section Gap) |
|---|---|---|---|---|---|
| **移动端 (Mobile)** | `< 768px` (基准 375px) | `20px` | 4 列 | `16px` | `64px` |
| **平板 (Tablet)** | `>= 768px` | `60px` | 6 列 | `16px` | `64px` |
| **小桌面 (Desktop)**| `>= 1024px` | `60px` | 6 列 | `16px` | `80px` |
| **大桌面 (Large)** | `>= 1200px` | `60px` | 6 列 | `16px` | `80px` |

*(注：全尺寸状态下，槽宽 Gutter 始终保持 16px 不变。)*

### 4.3 布局 Token 变量参考 (CSS Variables)

AI 在编写代码时，必须使用以下标准变量（或在心中构建此映射），避免写死硬编码：

```css
/* 断点变量 (用于 @media) */
--screen-md: 768px;
--screen-lg: 1024px;
--screen-xl: 1200px;

/* 间距与栅格变量 */
--container-max-width: 1200px;
--layout-padding-mobile: 20px;
--layout-padding-desktop: 60px;
--grid-gutter: 16px;
--section-gap-mobile: 64px;
--section-gap-desktop: 80px;

---

## 五、 基础视觉变量系统 (Foundational Visual Tokens)

除了颜色和字体，AI 在构建页面容器时，必须严格调用以下圆角和阴影 Token，严禁随意编造 px 数值。

### 5.1 圆角系统 (Border Radius) 与嵌套约束

| Token 变量 | 尺寸 (px) | 适用场景 |
|---|---|---|
| `--radius-sm` | `4px` | 极小元素：Tag 标签、Checkbox、Tooltip。 |
| `--radius-md` | `8px` | 中小元素：Button 按钮、Input 输入框、内部小图表。 |
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


## 六、 图标与文字排版规范 (Icon & Text Layout System)

页面中存在大量带有图标的按钮、列表项和说明文字。AI 在生成代码时，遇到“图标 + 文字”的组合，必须严格遵循以下布局关系与对齐法则：

### 6.1 左右排版 (Horizontal Layout)

这是最常见的图文组合形式（如带图标的列表项、普通按钮）。

*   **位置：** 图标默认位于文字的**左方**。
*   **间距 (Gap)：** 图标与文字之间的水平间距固定为 `8px`。
*   **对齐方式：**
    *   **单行文字：** 图标与文字实现绝对的垂直居中对齐。
    *   **⚠️ 多行文字 (折行状态)：** 当文字过长导致折成两行或三行时，**图标必须与第一行文字保持垂直居中对齐**，严禁与整个多行文本块居中对齐。

### 6.2 上下排版 (Vertical Layout)

常用于功能入口、大型特性卡片。

*   **位置：** 图标位于文字的**正上方**。
*   **间距 (Gap)：** 图标与文字之间的垂直间距固定为 `8px`。
*   **对齐方式：** 图标与文字整体**左对齐 (Left-aligned)**。

---

#### 💡[AI Agent 识别与生成规则]：多行图文对齐的 CSS 渲染指令

AI 在编写 HTML/CSS 结构时，为了完美实现上述规范，请强制遵守以下代码范式：

**1. 左右多行文字对齐（防错约束）：**
当遇到可能折行的左右图文结构时，**绝对禁止**直接使用 `align-items: center;`。必须采用 `flex-start` 结合首行行高计算，或直接给出标准 CSS 写法。

**✅ 强制参考 CSS 范式 (左右排版)：**
```css
.icon-text-horizontal {
  display: flex;
  flex-direction: row;
  align-items: flex-start; /* 重点：顶部对齐以适应多行 */
  gap: 8px;                /* 重点：水平间距 8px */
}

.icon-text-horizontal .icon {
  flex-shrink: 0;          /* 防止图标被文字挤压变形 */
  /* 重点：使用 margin-top 将图标推至与第一行文字(基于 line-height)视觉居中的位置 */
  /* 假设文字 line-height 为 24px，图标为 16px，则 margin-top = (24 - 16) / 2 = 4px */
  margin-top: 4px;         
}

---

## 七、 综合代码生成模板 (Integration Code Template)

为了确保 SurferCloud 官网的视觉统一性，AI 在生成业务模块（如：产品优势卡片、价格配置表单、数据中心列表）时，必须参考以下标准的 HTML/CSS 结构范式。

### 7.1 标准业务模块构建示范 (Feature Section Example)

此示例展示了如何综合应用“通栏/居中布局”、“卡片嵌套色彩”、“图文排版”以及“字体解耦”规则。

**✅ [正确代码范式]：**

```html
<!-- 1. 布局层：1920通栏背景 + 1200内容居中 -->
<section class="feature-section">
  <div class="content-container">
    
    <!-- 2. 文本层：正确的字体解耦与颜色调用 -->
    <div class="section-header">
      <h2 class="title">High-Speed Quant Finance Engine</h2>
      <p class="desc">Outstanding O Elastic Compute (UHost) provides robust support...</p>
    </div>

    <!-- 3. 栅格与卡片层：Grid 布局 + 卡片阴影/圆角 -->
    <div class="feature-grid">
      <div class="feature-card">
        
        <!-- 4. 图文对齐层：图标在左，垂直居中于第一行文字 -->
        <div class="card-title-wrap">
          <img class="icon" src="..." alt="icon" />
          <h3 class="card-title">Strategy Backtesting</h3>
        </div>
        
        <!-- 5. 嵌套层：卡片内的次级底托，使用更深的灰度形成 Z 轴对比 -->
        <div class="inner-data-panel">
          <span class="data-value">10 Million</span>
          <span class="data-label">Maximum PPS</span>
        </div>
        
      </div>
    </div>
    
  </div>
</section>

/* AI 必须使用以下变量组合方式编写 CSS */

/* 布局控制 */
.feature-section {
  width: 100%;
  background-color: #FFFFFF; /* Level 0 背景 */
  padding: var(--section-gap-desktop) 0;
}
.content-container {
  max-width: var(--container-max-width);
  margin: 0 auto;
  padding: 0 var(--layout-padding-desktop);
}

/* 字体与文本 */
.section-header .title {
  font-size: var(--font-size-h2);
  line-height: 1.25;
  font-weight: var(--font-weight-bold);
  color: var(--text-title);  /* 绝对禁止使用 background 的灰阶 token */
}
.section-header .desc {
  font-size: var(--font-size-body);
  font-weight: var(--font-weight-regular);
  color: var(--text-body);
}

/* 组件与嵌套色彩 */
.feature-card {
  background-color: var(--color-grey-1); /* Level 1 一级卡片浅灰背景 */
  border-radius: var(--radius-xl);       /* 默认 16px 圆角 */
  box-shadow: var(--shadow-sm);
  padding: 24px;
}
.inner-data-panel {
  background-color: var(--color-grey-2); /* Level 2 次级卡片，加深一阶 */
  border-radius: var(--radius-md);       /* 同心嵌套，圆角缩小到 8px */
}

/* 图文对齐法则 (左右多行结构) */
.card-title-wrap {
  display: flex;
  align-items: flex-start; /* 防止折行时图标居中悬空 */
  gap: 8px;
}
.card-title-wrap .icon {
  flex-shrink: 0;
  margin-top: 4px; /* 根据 line-height 计算的视觉居中补偿 */
}

## 八、 AI Agent 全局核心铁律 (Global Directives)

当接收到用户的 UI 生成、代码转换或组件设计指令时，AI 必须在后台运行以下安全检查逻辑。任何违反以下原则的代码将被视为**生成失败**：

- **[规则 1] 绝对禁止硬编码 (No Hardcoding)**
  颜色、字号、圆角、阴影必须 100% 映射到本文档定义的 `var(--xxx)` Token 或指定的 Hex 值，严禁出现规范外的魔术数字（如 `#333`, `font-size: 15px`）。

- **[规则 2] 严格守住 1200px 红线 (Layout Bounds)**
  除带有通栏背景的 `Wrapper` 容器外，所有的文本、交互按钮、业务卡片、表格，绝对禁止突破 `1200px` 的最大宽度限制。

- **[规则 3] Z轴层级色彩递进校验 (Z-Index Color Check)**
  只要出现卡片嵌套，内层底板的颜色必须比外层深一阶（例如：外层使用纯白，内层必须用 Grey 1；外层用 Grey 1，内层必须用 Grey 2）。

- **[规则 4] 字体三维解耦拼装 (Typography Decoupling)**
  禁止给 HTML 标签绑定死板的字体样式。必须将 `font-size` (尺寸)、`font-weight` (粗细)、`color` (文本专属颜色) 作为三个独立变量进行组合声明。

- **[规则 5] 无障碍与对比度红线 (Contrast Rule)**
  只要父级背景使用了品牌主色（如 `--color-blue-primary`）或品牌渐变色，其内部包裹的任何文本和图标必须强制切换为反白色 `--text-inverse`。

## 九、版本历史

| 版本 | 日期 | 更新内容 |
|------|------|----------|
| 1.0 | 2026-04-24 | 初始版本，基于 SurferCloud 设计规范图片创建 |

---

*本文档由 SurferCloud 设计团队维护，AI 代理在生成网页时应严格遵循此规范。*
