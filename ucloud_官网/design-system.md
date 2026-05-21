# ucloud 官网网页设计规范（与 www-v2 仓库对齐版）

> 本文档定义 ucloud 官网（仓库 `git@git.ucloudadmin.com:www/www-v2.git`）的网页设计规范，已与项目实际代码（`tailwind.config.ts`、`src/styles/globals.css`、`src/components/Button/*`、`src/components/CommonLayout.tsx`）完全对齐。
> 💡 [AI Agent 核心铁律]：生成代码时，**优先复用项目已存在的 CSS 变量、Tailwind 简写色、@layer 工具类与 React 组件**，严禁自行发明 token、严禁硬编码 HEX/像素值（已被 token 覆盖的部分）。

> 🚨 **[零号铁律 · 优先级最高 · 默认文案左对齐]**
> 所有 AI 生成的页面、区块、Hero、卡片、表单、列表、CTA 组——**文字、按钮、图文组合一律默认左对齐**：`text-left` / `items-start` / `justify-start`。
> **唯一允许居中的条件**：用户在**当前对话**中**显式书面要求**使用「居中 / 水平居中 / center / 让 XX 居中」等明确指令；此时才可用 `text-center` / `items-center` / `justify-center` / `mx-auto`（针对文本与图文组合）。
> ❌ **以下情况一律视为生成失败**（违反本条优先级高于其它一切视觉直觉）：
>  - 「Hero 区域我觉得居中更有冲击力」「营销页惯例都是居中」「这个卡片内容少居中好看」——任何**自我推断**的居中
>  - 沿用 v0/某模板的居中布局却没有得到对话中明确许可
>  - 把单个孤立按钮 `mx-auto` 居中（除非用户明确要求）
> ✅ **不受本条限制的居中**（属于布局机制，非「文案居中」）：
>  - 容器整体水平居中（`.adaptive-content-wrap` / `.content-wrap` 自带的 `mx-auto`，作用于 max-width 1440 容器本身）
>  - 行内元素与图标的**纵向对齐**（`items-center` 用于 flex 行内 icon 与文字基线对齐时）
>  - 表格单元格、Tag、Badge 等**原子组件内部**的字符居中

---

## 〇、项目架构概览（Stack & Conventions）

| 项 | 说明 |
|---|---|
| **框架** | Next.js 14（App Router，`src/app/...`） |
| **样式方案** | Tailwind CSS 3.3 + SCSS Module（`*.module.scss`）+ 全局变量（`src/styles/globals.css`） |
| **UI 组件库** | `@ucloud-fe/react-components`、`antd@5`；图标用 `@ucloud/ucloud-icons`（class 形式：`icon__xxx`） |
| **PC/响应式切换** | `<CommonLayout isResponsive>`：默认 PC（`body min-w-[1346px]`）；`isResponsive=true` 才走移动端断点 |
| **目录约定** | 公共组件 `src/components/`、页面 `src/app/...`、产品页模板 `src/product_template/`、纯 H5 `src/app/h5/`、`src/mobileComponents/` |
| **像素策略** | 大量使用 Tailwind 任意值（如 `h-[48px]`、`text-[16px]`、`rounded-[10px]`、`leading-[25px]`）；这是仓库既定写法，**不要改造为预设比例尺**。 |

> 🔥 [AI Agent 规则] 任何新页面/区块，**外层布局必须复用 `<CommonLayout>` 或落入已有 `(main)` / `site/...` 路由组**，禁止自带 `<html><body>`。

---

## 一、颜色系统（Color System）

### 1.1 真实的 CSS 变量清单（来自 `src/styles/globals.css :root`）

| 分类 | CSS 变量 | 值 | Tailwind 简写（在 `tailwind.config.ts` 中的映射） |
|---|---|---|---|
| **品牌主色** | `--primary-1` | `#3860f4` | `text-primary` / `bg-bgColor-blue` / `border-lineColor-blue` / `text-textColor-blue` |
| **白** | `--white` | `#ffffff` | `text-textColor-white` / `bg-bgColor-white` / `border-lineColor-white` |
| **标题文本** | `--text-title` | `#1D273F` | `text-textColor-title` |
| **正文文本** | `--text-body` | `#50627F` | `text-textColor`（DEFAULT） |
| **辅注文本** | `--text-remark` | `#c3cad9` | `text-textColor-remark` |
| **禁用文本** | `--text-disable` | `#bbbbbb` | `text-textColor-disable` |
| **页面/区块背景 1** | `--bg-gray-1` | `#F6F8FD` | `bg-bgColor-gray1` |
| **强调浅蓝背景** | `--bg-gray-2` | `#ECF0FF` | `bg-bgColor-gray2` |
| **极浅灰背景** | `--bg-gray-3` | `#F9FAFE` | `bg-bgColor-gray3` |
| **描边-标准** | `--line-gray-1` | `#DDE3F2` | `border-lineColor`（DEFAULT） / `bg-bgColor-gray4` |
| **描边-浅** | `--line-gray-2` | `#ECEFF6` | `border-lineColor-gray2` |
| **描边-中** | `--line-gray-3` | `#E1E6F0` | （通过 `bg-bgColor-gray3` 引用） |
| **按钮描边** | `--line-button` | `#E6EAF4` | `border-lineColor-button` |
| **深色辅助** | `--subColor-2A315F` | `#2A315F` | 直接 `bg-[var(--subColor-2A315F)]` |
| **辅助蓝 A1/A2** | `--subColor-1D89F2` / `--subColor-9DD6FF` | `#1D89F2` / `#9DD6FF` | 用于辅助渐变 A 端点 |
| **辅助蓝 B1/B2** | `--subColor-4C70F5` / `--subColor-9DBBFF` | `#4C70F5` / `#9DBBFF` | 用于辅助渐变 B 端点 |
| **辅助青 C1/C2** | `--subColor-1DBEF2` / `--subColor-9DE2FF` | `#1DBEF2` / `#9DE2FF` | 用于辅助渐变 C 端点 |

#### 💡 [AI Agent 识别规则] Tailwind 简写 vs 变量直引
- **能用 Tailwind 简写就用简写**：`text-textColor-title`、`bg-bgColor-gray1`、`border-lineColor`。
- **没有简写的（如 `--subColor-*`、`--bg-gray-2`/`--text-body` 的某些场景）**：用 `text-[var(--xxx)]` / `bg-[var(--xxx)]`。
- **严禁硬编码**：禁止出现 `#3860f4`、`#1D273F`、`#F6F8FD` 等已被变量覆盖的字面 HEX。

### 1.2 渐变与辅助色（不在 token 中，需用任意值写）

| 用途 | CSS |
|---|---|
| **主品牌渐变（Hero/CTA 背景）** | `linear-gradient(90deg, #3860F4 0%, #4E8CFF 50%, #B5E6FF 100%)` |
| **`.gradient-title`（文字渐变蓝）** | 已在 `globals.css` 提供，直接加 `className="gradient-title"` |
| **`.gradient-title.red`（文字渐变红紫）** | 已提供，加 `className="gradient-title red"` |
| **`.button-gradient-red`（橙红按钮背景）** | 已提供，直接加 `className="button-gradient-red"` |
| **辅助渐变 A（蓝）** | `linear-gradient(90deg, var(--subColor-1D89F2) 0%, var(--subColor-9DD6FF) 100%)` |
| **辅助渐变 B（深蓝）** | `linear-gradient(90deg, var(--subColor-4C70F5) 0%, var(--subColor-9DBBFF) 100%)` |
| **辅助渐变 C（青）** | `linear-gradient(90deg, var(--subColor-1DBEF2) 0%, var(--subColor-9DE2FF) 100%)` |

### 1.3 [AI Agent 识别与生成规则] 文字色三铁律

1. **强对比定律**：标题强制 `text-textColor-title`，正文强制默认色（`text-textColor` 或 `text-[var(--text-body)]`）。禁止把整个模块的文字统一刷成单一颜色。
2. **交互可见性**：任何承载点击的 `<a>` / 文字按钮必须显式 `text-[var(--primary-1)]`（或 `text-textColor-blue`），不要继承父级灰色。可用现成类：`.btn-word-link`（默认深色 → hover 变主蓝）、`.btn-word-link-bule`（默认就是主蓝）、`.btn-word-link-bule-sm`（14px 主蓝）。
3. **深色底反白**：当父级是深色（`bg-[var(--subColor-2A315F)]`、深色渐变、Footer）时，内部所有文字/图标必须强制 `text-textColor-white`，不能让 `:root` 的深色文字色透过去。

---

## 二、字体系统（Typography）

### 2.1 字体栈（来自 `src/styles/globals.css body`）

```css
font-family: "PingFang SC", "Hiragino Sans GB", "微软雅黑", "Microsoft Yahei",
             tahoma, arial, "宋体";
```
另：`Blanch`（仅用于英文数字大标，`className="en3"`）。

### 2.2 ⚠️ 非标准 font-weight 比例（极易踩坑）

仓库在 `tailwind.config.ts` 内**重写了** `fontWeight` 比例，与 Tailwind 默认值完全不同。**AI 生成代码时必须按本表理解**：

| Tailwind 类 | 实际 CSS `font-weight` | 用途 |
|---|---|---|
| `font-extra-light` | **100** | 极少用 |
| `font-light` | **400** | 常规正文（≈别处的 `normal`） |
| `font-normal` | **500** | 中等强调（≈别处的 `medium`） |
| `font-medium` | **600** | 强调（≈别处的 `semibold`） |
| `font-bold` | **700** | 加粗 |
| `font-extra-bold` | **900** | 大号主标题（基础层 h1-h5 默认） |

> 🔥 [生成铁律] 不要按惯性写 `font-normal` 以为是 400 ——在本仓库它是 **500**。要写真正的 400，请用 `font-light`。

### 2.3 基础层标题样式（`@layer base` 已自动应用，无需重复声明）

| 标签 | 实际样式（已在 `globals.css` 中自动应用） |
|---|---|
| `<h1>` | `text-[60px] font-extra-bold text-textColor-title leading-normal` |
| `<h2>` | `text-[36px] font-extra-bold text-textColor-title leading-normal` |
| `<h3>` | `text-[36px] font-extra-bold text-textColor-title leading-normal` |
| `<h4>` | `text-[24px] font-extra-bold text-textColor-title leading-normal` |
| `<h5>` | `text-[14px] font-extra-bold text-textColor-title leading-normal` |

> 💡 [AI 生成提示] 直接用 `<h1>~<h5>` 即可继承上述样式；若要变体（如 `h2` 用作 36px/medium 副标），可叠加 `font-normal` 或 `font-medium` 覆盖 `font-extra-bold`。

### 2.4 模块内常用文字层级（不在基础层，按需 className）

| 用途 | 推荐写法 | 备注 |
|---|---|---|
| **导语 / 副标题** | `text-[16px] leading-normal text-textColor`（或现成 `className="subtitle"`） | `.subtitle` 已在 `globals.css @layer utilities` 中提供 |
| **正文（默认）** | `text-[14px] leading-[25px] font-light text-textColor` | 25px 行高是设计稿规范，保持原子写法 |
| **辅注 / 12px 提示** | `text-[12px] leading-normal text-textColor-remark` | 表单提示、版权信息 |
| **文字链接** | `<WordLinkButton>` 或 `<a className="btn-word-link">` | 自带 hover 主蓝、箭头位移 |

### 2.5 [AI Agent 生成校验] 段落组合三铁律

1. **标题与正文成对出现时**，标题用 `text-textColor-title`，正文用 `text-textColor`（DEFAULT，即 `--text-body`），**不要给同一段落统一刷一种灰**。
2. **行高与字号绑定**：14px 正文 → `leading-[25px]`；16px 副标 → `leading-normal`；12px 辅注 → `leading-normal`。
3. **链接语义强制覆盖父级颜色**：见 §1.3。

---

## 三、段落与间距系统（Spacing）

> 仓库**没有** spacing token，全部使用 Tailwind 任意值（`mt-[24px]`、`gap-[32px]` 等）。下表是**设计稿规定的固定间距**，AI 生成时直接落到任意值即可。

### 3.1 全局对齐定律（呼应零号铁律）

- **默认左对齐**：所有标题/正文/CTA/图文卡 → `text-left` / `items-start` / `justify-start`。
- **不得自动居中**：除非当前对话**显式要求**（「居中」/「center」/「让 XX 水平居中」），否则一律不得使用 `text-center` / `items-center` / `justify-center` / `mx-auto`（针对内容元素，不含 1440 容器自身）。详见文档顶部的零号铁律。
- **图文行内 flex** 需要图标与文字基线对齐时，`items-center` 是布局机制不算「文案居中」，可正常使用。

### 3.2 段落内（标题 → 正文 → 链接/按钮）垂直间距

| From → To | 间距 | Tailwind 写法 |
|---|---|---|
| 标题 → 正文 | `8px` | `mt-[8px]` 或 `gap-[8px]` |
| 正文 → 文字链接 | `24px` | `mt-[24px]` 或 `gap-[24px]` |
| 正文 → 独立大按钮 | `32px` | `mt-[32px]` |
| 大图标（≥68px）→ 标题 | `24px` | `mb-[24px]` 或 `gap-[24px]` |
| 小图标（<68px）→ 右侧标题 | `12px` | `gap-[12px]` |

### 3.3 水平 / 块间间距

| 场景 | 间距 |
|---|---|
| 文字链接 → 右侧箭头 | `6px`（在 `WordLinkButton` 内默认 `ml-[6px]`，hover 时 `translate-x-1`） |
| 卡片网格 gap（PC） | `32px` → `gap-[32px]` |
| 卡片网格 gap（≤1439px） | `24px` |
| 卡片网格 gap（≤767px） | `16px` |
| 模块上下区块（section） | `my-[80px]`（已提供 `.content` 工具类） |

### 3.4 [AI 生成铁律] 用 Flex/Grid + gap，不用 margin 堆栈

```tsx
<section className="content"> {/* my-[80px] */}
  <div className="adaptive-content-wrap"> {/* 见 §四 */}
    <div className="flex flex-col items-start">
      <h2>2级标题</h2>
      <p className="mt-[8px] text-[14px] leading-[25px] font-light">正文……</p>
      <a className="btn-word-link mt-[24px]">了解详情<span className="icon__arrow-right" /></a>
    </div>
  </div>
</section>
```

---

## 四、布局与栅格（Layout & Grid）

### 4.1 满屏背景 + 居中定宽容器（双层结构）

仓库已经提供 **两种现成容器类**，直接复用，**严禁自行硬编码 `width: 1920px`**：

| 工具类 | 来源 | 等价 Tailwind | 适用场景 |
|---|---|---|---|
| `.adaptive-content-wrap` | `globals.css @layer utilities` | `px-[22px] xsm:px-[60px] w-full mx-auto max-w-[1440px]` | **响应式页面**（`isResponsive=true`）：移动端 22px 留白、≥768px 60px 留白 |
| `.content-wrap` | `globals.css @layer utilities` | `px-9 mx-auto max-w-[1440px] min-w-[1280px] box-border` | **纯 PC 页面**：左右 36px、锁死 1280–1440px |
| `.content` | `globals.css @layer utilities` | `my-[80px]` | 区块上下间距 |

```tsx
// 推荐写法（响应式产品页）
<section className="bg-[url('/banner.jpg')] bg-cover bg-center">  {/* 满屏背景层 */}
  <div className="adaptive-content-wrap content">                  {/* 居中定宽层 + 上下间距 */}
    ...
  </div>
</section>
```

### 4.2 真实断点（来自 `tailwind.config.ts.screens`）

| 别名 | 触发宽度 | 典型用途 |
|---|---|---|
| `xxsm` | ≥ 375px | 移动端起点 |
| `xsm` | ≥ 768px | 平板 / 横屏手机 |
| `sm` | ≥ 1024px | 小桌面 |
| `md` | ≥ 1200px | 中桌面 |
| `l` | ≥ 1300px | 中大桌面 |
| `lg` | ≥ 1440px | 标准桌面（设计稿基准） |
| `xlg` | ≥ 1920px | 2K+ 大屏 |

> 🔥 [AI 生成铁律] 直接用上述别名，**禁止再写 Tailwind 默认断点的直觉**（默认 `sm` = 640px、`md` = 768px 在本仓库**全被覆盖**）。

### 4.3 响应式栅格降级公式（Grid Reflow）

PC 主流栅格在小屏上的降级：

| PC 列数 | ≥1440 (`lg`) | ≥1024 (`sm`) | ≥768 (`xsm`) | <768 |
|---|---|---|---|---|
| **4 等分** | 4 | 2 | 2 | 1 |
| **3 等分** | 3 | 3 | 1 或横滑 | 1 |
| **2 等分** | 2 | 2 | 1 | 1 |

```tsx
// 推荐写法
<div className="grid grid-cols-1 xsm:grid-cols-2 sm:grid-cols-2 lg:grid-cols-4 gap-[16px] xsm:gap-[24px] lg:gap-[32px]">
  ...
</div>
```

### 4.4 PC 锁死页面与响应式页面的区别

- **PC 锁死**：`CommonLayout` 不传 `isResponsive` → `body` 自动加 `min-w-[1346px]`。这是 `(main)` 路由组的默认行为。这种页面里**只用 `.content-wrap`**，不用 `.adaptive-content-wrap`。
- **响应式**：在 `LayoutProvider` 或 `CommonLayout` 上传 `isResponsive` → 移除 `min-width`，全程用 `.adaptive-content-wrap` + `xxsm/xsm/sm/...` 断点。

---

## 五、形状与阴影（Borders, Radius & Shadow）

仓库**没有** `--radius-*` / `--shadow-*` token，请直接用 Tailwind 任意值或既有简写。

### 5.1 圆角（Radius）实战参考

| 元素 | 圆角 |
|---|---|
| 标签 / Tooltip / Checkbox | `rounded-[4px]` |
| 输入框 / 小图表 | `rounded-[8px]` |
| 按钮（全场景统一） | `rounded-[10px]` ⬅ **强制** |
| 次级容器 / 嵌入卡 | `rounded-[12px]` |
| 大卡片 / Modal | `rounded-[16px]` |
| Hero 大背景板 / 浮层 | `rounded-[20px]` ~ `rounded-[24px]` |
| 头像 / 胶囊按钮 | `rounded-full` |

> 💡 [同心圆角铁律] 容器内嵌容器时，**内层 radius < 外层 radius**：内 ≈ 外 − padding。如外层 `rounded-[16px] p-[8px]`，内层用 `rounded-[8px]`。

### 5.2 边框色

- 默认 `border border-lineColor`（`#DDE3F2`）
- 按钮 `border border-lineColor-button`（`#E6EAF4`）
- 浅 `border border-lineColor-gray2`（`#ECEFF6`）

### 5.3 阴影（仓库唯一已定义阴影）

```ts
// tailwind.config.ts extend.boxShadow
'card-shadow': '0px 16px 16px 0px rgba(235, 240, 252, 0.19)'
```
用法：`shadow-card-shadow`（已被大量卡片复用）。需要其它阴影一律用任意值 `shadow-[0_4px_4px_-2px_rgba(23,25,49,0.04)]`，**不要再造新 token**。

---

## 六、按钮系统（Buttons）

### 6.1 直接复用现有按钮类（来自 `globals.css @layer components`）

| 尺寸类 | 高度 | 内距 | 圆角 | 字号 |
|---|---|---|---|---|
| `.btn-sm` | `h-[42px]` | `px-[16px]` | `rounded-[10px]` | `16px` |
| `.btn-md` | `h-[48px]` | `px-[24px]` | `rounded-[10px]` | `16px` |
| `.btn-lg` | `h-[52px]` | `px-[24px]` | `rounded-[10px]` | `16px` |

| 变体类 | 视觉 | 适用 |
|---|---|---|
| `.btn-halo-blue` | 主蓝实底 + 鼠标光晕 | 主 CTA |
| `.btn-halo-yellow` | 橙红渐变 + 光晕 | 营销活动 |
| `.btn-halo-red` | 纯红实底 + 光晕 | 警示 / 促销 |
| `.btn-halo-white` | 白底红字 | 红色背景上的次按钮 |
| `.btn-border-white` | 白底灰描边，hover 蓝边蓝字 | 次按钮 |
| `.btn-white-border` | `52px` 白底灰描边 + flex space-between | 卡片底部固定高度按钮 |
| `.btn-word-link` | 深色文字 + hover 主蓝 | 段落末尾「了解详情 →」 |
| `.btn-word-link-bule` | 主蓝文字（16px） | 强调链接 |
| `.btn-word-link-bule-sm` | 主蓝文字（14px） | 卡片内链接 |

> ⚠️ `.btn-halo-*` 必须与 `<HaloButton>` 配合才能出现鼠标跟随光晕效果（光晕由 React 组件维护）。

### 6.2 推荐 React 组件（已封装好交互）

```tsx
import HaloButton from '@/components/Button/HoverHaloButton';
import WordLinkButton from '@/components/Button/WordLinkButton';

// 主 CTA：48px 主蓝光晕按钮
<HaloButton
  buttonClassName="btn-md btn-halo-blue w-[230px]"
  icon="icon__arrow-right"
  onClick={...}
>立即购买</HaloButton>

// 大号主 CTA：52px
<HaloButton buttonClassName="btn-lg btn-halo-blue w-[283px]" icon="icon__arrow-right">
  免费试用
</HaloButton>

// 次按钮（无光晕、纯描边）
<a href="..." className="btn-md btn-border-white">了解详情</a>

// 文字链接（带箭头位移动画）
<WordLinkButton link="/foo" icon="icon__arrow-right">了解更多</WordLinkButton>
```

### 6.3 [AI 生成铁律] 按钮三禁

1. **禁止** 写新尺寸 —— 高度必须是 42 / 48 / 52，圆角必须是 `10px`。
2. **禁止** 用裸 `<button>` 实现主 CTA —— 必须用 `<HaloButton>` 才有官网统一的鼠标光晕。
3. **禁止** 在按钮上叠 `font-bold` —— 仓库按钮统一不加粗（继承 light / normal）；如需强调用 `font-medium`（= 600）。

---

## 七、其它已就绪的工具类速查

| 类名 | 用途 |
|---|---|
| `.subtitle` | 16px 副标题 |
| `.gradient-title` | 文字主蓝渐变 |
| `.gradient-title.red` | 文字红紫渐变（营销页用） |
| `.button-primary` | 100% 宽度的主蓝按钮（在某些产品卡片底部使用） |
| `.button-gradient-red` | 橙红渐变背景（小标签 / 胶囊用） |
| `.common-transition` | 标准过渡（300ms 100ms delay cubic-bezier(0,0,0.2,1)） |
| `.text-transition` | 文字过渡（100ms） |
| `.multi-Twoline-ellipsis` | 2 行截断 |
| `.multi-line-ellipsis` | 3 行截断 |
| `.card_header_tag` | 卡片右上角折角徽章（带 ::before / ::after 装饰） |
| `.en3` | 英文标 Blanch 字体 |
| `.hot-tag` | 12px 红色「HOT」徽章 |

---

## 八、AI Agent 全局核心铁律（生成校验清单）

按以下顺序自检，违反任一项视为**生成失败**：

1. **【容器】** 是否落到了 `.adaptive-content-wrap` / `.content-wrap` 之一？没有 → 失败。
2. **【颜色】** 是否所有颜色都走 Tailwind 简写（`text-textColor-title`、`bg-bgColor-gray1`、`border-lineColor`、`text-primary`）或 `var(--xxx)`？出现裸 `#xxxxxx`（且该值在 §1.1 表中）→ 失败。
3. **【字重】** `font-normal` 是否被当作 400 使用？是 → 失败（它是 500，要 400 请用 `font-light`）。
4. **【按钮】** 主 CTA 是否走 `<HaloButton>` + `btn-md/lg` + `btn-halo-blue`？高度不是 42/48/52、圆角不是 `10px` → 失败。
5. **【断点】** 是否用了 `xxsm/xsm/sm/md/l/lg/xlg`？沿用 Tailwind 默认 `sm:` = 640 的直觉（本仓库 `sm` = 1024）→ 失败。
6. **【深色底反白】** 深色 `section` 内文字是否强制 `text-textColor-white`？没有 → 失败。
7. **【对齐】** 是否默认左对齐？无明确指令而自作主张 `text-center` → 失败。
8. **【图标】** 用的是 `<i className="icon__xxx" />` 还是 SVG / emoji？非 `icon__xxx` 类 → 失败（仓库统一用 `@ucloud/ucloud-icons`）。
9. **【布局工具】** 多元素间距是否用 `flex / grid + gap-[Npx]` 而非堆叠 `margin`？大量 `mt-[*]` 串联 → 失败。
10. **【组件复用】** 段落末尾「了解详情 →」是否用 `<WordLinkButton>` 或 `.btn-word-link`？自己手写 `<a>+<span>` → 失败。

---

## 版本历史

| 版本 | 日期 | 更新内容 |
|------|------|----------|
| 2.0  | 2026-05-21 | 全量重构：与 `www-v2` 仓库的 `tailwind.config.ts` + `globals.css` + Button 组件对齐；删除虚构 token（`--color-primary`/`--radius-xl`/`--spacing-*`/`--shadow-md` 等），改为引用真实变量（`--primary-1`/`--text-title`/`--bg-gray-1`/`--line-button`/`--subColor-*`）；纠正字重比例（`font-normal` = 500 非 400）；纠正断点（`xxsm/xsm/sm/md/l/lg/xlg`）；纠正按钮尺寸（42/48/52，圆角 10px）；新增 §〇 项目架构与 §八 生成自检清单。 |
| 1.0  | 2026-05-11 | 初始版本，基于 ucloud 设计稿图档创建（与代码未对齐）。 |
