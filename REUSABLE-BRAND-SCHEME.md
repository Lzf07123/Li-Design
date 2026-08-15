# Li& 系列 · 可复用品牌设计方案

> **版本**：V1.1 ｜ **日期**：2026-08-16 ｜ **状态**：可复用基准（后续项目以此为起点实例化；V1.1 新增第 8 章多 Agents 协作方法）
> **存放位置**：独立模板仓库，可置于任意位置（与各子项目同级或克隆到其他机器），供所有子项目共用参考。
> **提取来源**：Li&Pass 现有设计系统——BRAND.md（品牌意图）、MASTER.md（实现速览）、`index.css`（代码事实）、`brand.ts`（品牌资产）——已提炼内联于本文档，不依赖源仓库路径。
> **配套文件**：[reusable-tokens.template.css](reusable-tokens.template.css)（复制、改前缀、填色值后即可用）、[AGENTS.md](AGENTS.md)（模板仓库的多 Agents 协作手册，与第 8 章配合使用）。
> **使用边界**：本仓库仅在项目第一次设计时参考；首次设计完成后必须在项目内生成适用方案（见 §1.1、§1.2），后续开发以项目内方案为准。

---

## 1. 用途与使用方式

本方案把 Li&Pass 已打磨成熟的品牌设计抽象成**三层结构**，让后续项目（Li&Chat 及新立项）不用从零设计，也不至于生搬硬套：

| 层 | 内容 | 复用方式 |
| --- | --- | --- |
| 品牌内核（不变层） | 人格公式、五大原则、几何符号语法、动效呼吸感、文案语调、治理结构 | 第 2 章，直接继承，除非有明确理由才改 |
| 项目适配层（槽位层） | 项目名、定位、主色、中性色、语义色、字体、Logo、令牌前缀、主题键 | 第 3 章，逐槽位重填 |
| 落地模板（执行层） | 令牌骨架 CSS、组件清单、页面外壳、验收清单 | 第 4–6 章，复制并按清单执行 |

三种典型使用场景：

- **新项目启动**：先做第 3 章「填槽位」，再走第 4 章「实例化流程」，最后过第 6 章验收。
- **存量项目对齐**：用第 6 章清单做差距审计，把第 2 章内核与第 5 章组件模式逐步对齐。
- **多 Agents 协作实例化**：按第 8 章把首次设计拆成 T1–T7 任务单元派活，root agent 验收后交付。

> 本文档面向「Li& 系列」产品家族；若某个项目需要独立品牌，至少保留第 2.2 节五大原则、第 2.4 节动效铁律与第 6 章无障碍/性能条款，其余可按需放开。

---

### 1.1 使用边界（重要）

> 本仓库只在项目**第一次设计**时作为参考起点。首次设计完成后，必须把结果实例化为**当前项目自己的设计方案**（见 1.2），后续所有开发与视觉决策以项目内方案为准；本仓库仅用于模板升级时的对照，不作为任何项目的运行时依赖。

### 1.2 首次设计必交产出（在项目内生成）

| 产出物 | 位置 | 说明 |
| --- | --- | --- |
| 项目品牌方案 | `design-system/<project>/BRAND.md` | 第 2 章品牌内核 + 第 3 章已填槽位的项目版 |
| 实现速览 | `design-system/<project>/MASTER.md` | 令牌、组件、页面模式的落地快照 |
| 令牌落地 | `frontend/src/index.css` | 复制 [reusable-tokens.template.css](reusable-tokens.template.css)、换前缀、填色值 |
| 品牌单点 | `frontend/src/lib/brand.ts` | 名称 / slogan / Logo / 备案的唯一出处 |
| 项目协作手册 | `AGENTS.md`（项目根） | 参照本仓库 [AGENTS.md](AGENTS.md) 与第 8 章，写下该项目的多 Agents 协作规范 |

## 2. 品牌内核（跨项目不变层）

### 2.1 定位公式与人格

**定位公式**：可信工具类产品 = 「一次 {关键动作}，{触达范围}」。品牌的第一任务是**建立信任**，第二任务是**让信任显得毫不费力**。

| 维度 | 通用描述 | Li&Pass 实例 |
| --- | --- | --- |
| 一句话定位 | 一次关键动作，通行触达范围 | 一次注册，通行所有授权网站 |
| 人格关键词 | 安全、可信、克制、专业、流畅 | 同左 |
| 人格比喻 | 一位可靠的守门人：不说废话、不制造惊吓，把门打开后安静退到一旁 | 同左 |
| 品牌承诺 | 一次验证，永久通行；每一步都被审计、每一次授权都明示 | 同左 |
| 避免成为 | 花哨的营销页、吓唬人的安全警告、冷冰冰的政务系统 | 同左 |

### 2.2 五大设计原则（TRUST 内核）

1. **信任优先（Trust First）**：色彩、字体、徽章、文案都传递「安全但不唬人」。安全提示清晰可行动，避免恐吓式文案；关键安全能力用可见但克制的方式呈现。
2. **克制的科技感（Restrained Tech）**：中性底色 + 单一主色强调，不用霓虹渐变、不用 AI 紫粉、不做夸张玻璃拟态。科技感来自干净、精确与动效质感，而不是色彩浓度。
3. **以动衬静（Motion as Breath）**：入场动效是一次性「打招呼」，环境循环动效是恒定的「呼吸」。所有氛围动效极慢、极淡、GPU 加速、永不阻塞交互；尊重 `prefers-reduced-motion`，低端设备自动降级。
4. **单一事实来源（Single Source of Truth）**：颜色/间距/阴影/动效只存在 `index.css` 的令牌里；品牌文案与资源只存在 `lib/brand.ts` 里。组件内禁止硬编码 hex 值与文案。
5. **无障碍与节能（Accessible & Efficient）**：正文对比度 ≥ 4.5:1，键盘焦点始终可见，可点击目标 ≥ 44×44px 或等价热区，动效尊重系统减弱偏好，移动端减量省电。

### 2.3 视觉语法：几何暗线

品牌氛围层的所有装饰元素都来自同一隐喻——**身份凭证安全地穿行**。符号规则跨项目通用，各项目只需重映射符号含义（见 3.2 槽位 6）：

| 符号 | 通用语义 | Li&Pass 映射 | 通用用法 |
| --- | --- | --- | --- |
| 细直线 | 连接与路径 | 通行 | 背景层低频穿行 |
| Z 形折线 | 门径 / 路线转折 | 品牌签名形 | 认证页 2–3 个，其余页面最多 1 个 |
| 方块 | 凭证 / 授权票据 | 授权票据 | 往复钟摆，稳定存在感 |
| 锁钥组合 | 安全与钥匙 | 安全 | 稀有元素，仅在信任关键时刻出现 |
| 圆点光斑 | 会话 / 数据包 | 会话 | 盘旋公转，活跃但安静 |

**符号铁律（跨项目不变）**：永远低透明度（0.04–0.25）、永远在背景层、几何、无渐变、描边或纯色、无阴影、无滤镜；是「品牌暗线」而非主角；绝不与文字、按钮、表格发生可读性冲突；绝不作为功能图标。

### 2.4 氛围动效：呼吸感四模式

入场动画只出现在页面出现的一瞬间；品牌氛围真正需要的是**恒定背景音**——极慢、极淡、永不停止的几何元素循环。核心哲学四条：永不退场（无限循环）、交错节奏（animation-delay 错峰）、用户无感（操作时几乎注意不到）、永不阻塞（只动 `transform/opacity`）。

| 模式 | 运动逻辑 | 适用元素 |
| --- | --- | --- |
| A 水平无限穿行 | 屏外左侧进入 → 水平穿越 → 移出右侧后重置；边缘淡入淡出 | Z 形飘片（大）、几何线条 |
| B 往复钟摆 | 固定距离内来回（`alternate`），不离开屏幕 | 正方飘块、Z 形飘片（小） |
| C 正弦波形 | 水平匀速 + 垂直正弦起伏，穿越后重置 | 锁钥组合 |
| D 盘旋公转 | 绕自身中心或屏幕某点做 360° 旋转 / 椭圆公转 | 圆点光斑 |

**执行铁律（跨项目不变）**：

- 所有飘动元素 `animation-iteration-count: infinite`，`animation-fill-mode: both`，`pointer-events: none`，`will-change: transform, opacity`。
- 只动 `transform/opacity`；严禁触发回流；动画元素禁用 `filter` 与 `box-shadow`。
- 错峰公式：`animation-delay = (元素索引 / 总元素数) × 最大错峰时间 + 随机余量(±2s)`。
- 交互联动：表单聚焦时 `.is-typing` 使周期 ×2（速度减半）；列表页滚动越快飘动越快（0.5x–1.5x）。
- `prefers-reduced-motion: reduce` 时全部缩短为 `0.01ms` 单帧；移动端（<768px）元素数 ≤6、速度更慢、透明度更低。

典型参数区间（可在项目内微调，但保持「极慢极淡」的量级）：

| 元素 | 轨迹 | 单次周期 | 透明度 | 缩放 |
| --- | --- | --- | --- | --- |
| Z 形飘片（大） | A | 45s | 0.06–0.12 | 0.8–1.2 |
| Z 形飘片（小） | B | 30s | 0.10–0.18 | 0.5–0.8 |
| 正方飘块 | B | 40s | 0.06–0.10 | 0.6–1.0 |
| 圆点光斑 | D | 25s | 0.15–0.25 | 0.8–1.5 |
| 几何线条（长） | A | 60s | 0.04–0.08 | 1.0 |
| 锁钥组合 | C | 90s | 0.04–0.06 | 0.9–1.1 |

### 2.5 文案语调

- 清晰优先：先告诉用户发生了什么、下一步做什么（「我们已向 your@email.com 发送验证码」优于「验证码已发送」）。
- 动词开头的按钮：登录、注册、继续授权、保存更改、强制下线。
- 不用感叹号、不用网络流行语、不过度拟人化；信任场景需要平静的确定性。
- 错误信息可行动：「密码错误，请重试或点击忘记密码」优于「登录失败」。
- 安全语言诚实但不吓唬：直接说明事实并提供处置，不做恐吓式红色警报。
- 数字与时间精确：剩余尝试次数、锁定倒计时、验证码有效期都给出具体数值。

### 2.6 治理与单一事实来源

四级分层跨项目通用（把 `lipass` 换成项目 slug）：

| 层级 | 文件 | 职责 |
| --- | --- | --- |
| 品牌意图 | `design-system/<project>/BRAND.md` | 定位、原则、视觉方向、氛围动效标准 |
| 实现速览 | `design-system/<project>/MASTER.md` | 令牌、组件、页面模式的落地快照 |
| 代码事实 | `frontend/src/index.css` | 颜色/阴影/动效令牌的唯一出处 |
| 品牌资产 | `frontend/src/lib/brand.ts` + `frontend/public/` | 名称、slogan、Logo、备案的唯一出处 |

发生冲突时：**代码事实优先**（`index.css` / `brand.ts` 是运行时真相），但必须同步回写 MASTER.md 与 BRAND.md，防止文档漂移。

---

## 3. 项目适配层（槽位表）

新项目逐行填下表。第 2 章内核不动；本表是「可替换面」。填表时遵守 3.1–3.4 的通用取色与资产规则。

| # | 槽位 | 填写说明 | Li&Pass 现值（示例） |
| --- | --- | --- | --- |
| 1 | 项目显示名 | 对外展示名，统一一个写法 | `Li&Pass` |
| 2 | 技术标识 | 小写，贯穿 Cookie/kid/acr/目录/卷名，不再新增其他别名 | `lipass` |
| 3 | 一句话定位 | 按 2.1 定位公式 | 一次注册，通行所有授权网站 |
| 4 | 品牌承诺 | 一句可验证的长期承诺 | 一次验证，永久通行；每一步都被审计、每一次授权都明示 |
| 5 | 人格比喻 | 一位可靠的角色，克制、可靠 | 守门人 |
| 6 | 符号隐喻 | 沿用 2.3 五个符号，重映射语义 | 直线=路径、Z 形=门径、方块=凭证、锁钥=安全、光斑=会话 |
| 7 | 主色（浅） | 主色 / hover / soft / fg 四件套 | `#0369A1` / `#075985` / `#E0F2FE` / `#FFFFFF` |
| 8 | 主色（深） | 深色取去饱和浅色调变体（亮度 300–400 档） | `#38BDF8` / `#7DD3FC` / `rgba(56,189,248,0.14)` / `#082F49` |
| 9 | 中性色（浅） | bg / surface / surface-2 / fg / muted / border | `#F8FAFC` / `#FFFFFF` / `#F1F5F9` / `#0F172A` / `#64748B` / `#E2E8F0` |
| 10 | 中性色（深） | 同序 | `#0B1220` / `#111A2C` / `#1B2740` / `#E2E8F0` / `#94A3B8` / `#263449` |
| 11 | 语义色（浅/深） | 成功 / 警告 / 危险，及 soft 底色 | 见附录 B 令牌快照 |
| 12 | 焦点环 | 2px 主色描边 + 2px offset，`focus-visible` 全局生效 | 浅 `#0369A1`，深 `#38BDF8` |
| 13 | 字体栈 | 家族默认栈 + 中文回退；不加载远程字体 | Inter → 系统栈 → PingFang SC / 微软雅黑 |
| 14 | 可选标题字体 | 如需品牌辨识度，自托管（`font-display: swap` + subset），不做 CDN 引用 | Lexend（Corporate Trust 组合，仅页面标题） |
| 15 | Logo / favicon | 透明底 512×512 WebP 单格式；最小 32px；周围净空 ≥ 1/4 图标边 | `brand-logo.webp` / `favicon.webp` |
| 16 | 令牌前缀 | `index.css` 的 CSS 变量前缀，逐项目唯一 | `portal`（`--portal-bg` 等） |
| 17 | 主题存储键 | 首帧主题脚本与 `useTheme` 共用 | `portal-theme` |
| 18 | slogan / 备案 | 从 `brand.ts` 读取；备案上线前留空，禁止假占位号 | slogan + ICP/公安备案占位 |
| 19 | 氛围浓度 | 认证 / 授权 / 中心 / 后台的 shapeCount | 10 / 4 / 10 / 4（后台 opacity 0.5） |
| 20 | 浏览器品牌位 | favicon、`theme-color`（浅/深）、`description`、首帧主题脚本 | 见 `frontend/index.html` |

### 3.1 取色方法

- 主色按产品域选择：用 ui-ux-pro-max 规则库 `--design-system "<product> <industry> <keywords>"` 检索推荐，再按 WCAG AA 校验前后景对比（正文 ≥ 4.5:1，UI 组件 ≥ 3:1）。
- 用色比例约 **60/30/10**：中性色 ≈ 60%，表面内容 ≈ 30%，主色 + 语义色 ≈ 10%。主色永远是小面积强调，不做大面积主色背景。
- 语义色只表达状态，不用于装饰。
- 深色模式用**去饱和的浅色调变体**，不是简单反色；主色深色版取该色相 300–400 亮度档，soft 底色用 `rgba(主色, 0.12–0.16)`。
- 禁用清单：大面积 AI 紫粉渐变、霓虹渐变、纯黑 `#000`、低对比灰字、装饰性色块。低透明度的氛围点缀与卡片渐变描边除外（只出现在背景与描边层）。

### 3.2 资产规则

- Logo 禁止改色、旋转、加描边、拉伸、叠加文字；深色/浅色背景均使用同一透明底 Logo，不得反白处理。
- 图标统一内联 SVG（symbol 或组件内联 path），禁止 emoji 充当图标；基准 24×24 viewBox、1.5–2px 描边、圆角端点（对齐 Heroicons/Lucide 描边系）；颜色继承 `currentColor`，状态图标用语义色。

### 3.3 形状、间距与层次（通用默认值）

| 类别 | 规范 |
| --- | --- |
| 圆角 | 按钮/输入框 8px（`rounded-lg`）；卡片/弹窗 16px（`rounded-2xl`）；徽章 `rounded-full` |
| 间距 | 4px 基准刻度；卡片内边距 `p-6`（24px）起步，认证卡 `p-6 sm:p-8` |
| 阴影 | 三档弥散阴影 `--shadow-sm/md/lg`，透明度总和 < 0.1，禁止重投影 |
| 层级 | 顶栏 `z-20`、弹窗遮罩 `z-70`、Toast `z-80`（必须高于弹窗）；氛围层固定在内容下方 |
| 交互 | 可点击元素必须有 `cursor-pointer`；hover 上移 1px + 阴影过渡；按压 `scale(0.97)`；过渡 150–300ms |

---

## 4. 落地模板与实例化流程

### 4.1 新项目文件映射

| 新项目目标文件 | 来源 |
| --- | --- |
| `frontend/src/index.css` | 复制 [reusable-tokens.template.css](reusable-tokens.template.css)，全局替换 `{{PROJECT_PREFIX}}`，填入槽位 7–12、16 色值 |
| `frontend/src/lib/brand.ts` | 按本方案槽位 1、3、18 与 3.2 资产规则新建，名称/slogan/Logo/备案全部从此文件读取 |
| `frontend/index.html` | 按槽位 20 配置：favicon、明暗 `theme-color`、`description`、首帧主题脚本（存储键 = 槽位 17） |
| `frontend/public/` | 放入 `brand-logo.webp`、`favicon.webp`、备案徽章、`icons.svg` |
| `design-system/<project>/BRAND.md` + `MASTER.md` | 以本文档第 2 章为内核模板重写，记录项目槽位决策 |

### 4.2 实例化十步

1. **填槽位**：完整填写第 3 章槽位表（1–20 项），记录到 `design-system/<project>/BRAND.md`。
2. **铺令牌**：复制 `reusable-tokens.template.css` → `frontend/src/index.css`，替换前缀并填色值；`@theme` 只暴露语义别名（`bg-primary` 等），组件不直接引用 `--<prefix>-*`。
3. **建品牌单点**：按模板创建 `frontend/src/lib/brand.ts`，名称/slogan/Logo/备案全部从该文件读取。
4. **配浏览器品牌位**：`index.html` 配 favicon、明暗 `theme-color`、`description` 与首帧主题脚本（避免明暗闪烁），兜底背景色同步到令牌 bg。
5. **搭组件基座**：按第 5 章清单移植 `.btn` / `.card` / `.input` / `.badge` / `.notice` / `.modal` / `.toast` / `.table-shell` 等类；可点击元素补 `cursor-pointer`。
6. **搭页面外壳**：认证类页用居中单卡 `AuthShell`（`max-w-md` + 顶部品牌 + slogan + 底部备案）；已登录页用 `AppHeader` + `max-w-7xl` 内容 + `SiteFooter`；管理类用顶部标签页。
7. **接氛围层**：复用 Canvas 版 `FloatingBackground`（无第三方依赖），按槽位 19 设 `shapeCount`/`opacity`/`calm`/`scrollWind`/`adaptive`/`theme="auto"`；画布 `z-0` 垫底、`pointer-events: none`。
8. **接主题**：`useTheme` 读写槽位 17 的存储键，切换 `html.dark`；所有明暗差异只通过 `.dark` 令牌块表达。
9. **过验收**：执行第 6 章 Pre-Delivery Checklist 与动效验收清单。
10. **回写治理**：把最终令牌、组件、页面模式回写 `MASTER.md`，变更理由回写 `BRAND.md`。

### 4.3 页面氛围浓度分层

| 页面类型 | 外壳 | 氛围浓度 | 关键约束 |
| --- | --- | --- | --- |
| 认证页（登录/注册/找回/验证等） | `AuthShell`：居中 `max-w-md` 卡片 + 极光背景 + 顶部品牌 + 底部备案 | 高（默认 10） | 卡片及其上方 120px 禁飘；品牌名与 slogan 必须出现 |
| 授权/信任关键时刻 | `AuthShell` 变体 | 低（4） | 氛围减半；核心内容绝对清晰 |
| 用户中心/工作台 | `AppHeader` + `max-w-7xl` + `SiteFooter` | 中（10 + 滚动联动） | 卡片区域不遮字 |
| 管理后台 | `AppHeader` + 顶部标签页 | 极低（4 × opacity 0.5） | 表格区域完全禁飘 |

---

## 5. 组件与交互模式库（复用清单）

| 组件 | 类名 / 文件 | 复用要点 |
| --- | --- | --- |
| 按钮 | `.btn` 系列（primary/secondary/danger/ghost/link） | 主按钮用「主色 → 主色悬停」纵向渐变 + `background-position` 过渡；`disabled` 时 `opacity-50` |
| 卡片 | `.card`、`.card-signature`、`.card-interactive` | 认证卡用 padding-box 表面 + border-box 低饱和品牌渐变描边双背景 |
| 表单 | `.label` / `.input` / `.input-sm` | focus 主色边框 + `ring-2 ring-primary/20`；placeholder 用 `text-muted` |
| 徽章/提示条 | `.badge-*`、`.notice-*` | 语义色 + soft 底色；带状态图标 |
| 弹窗/Toast | `.modal-*`、`.toast-*` | Toast `z-80` 高于 Modal `z-70`；Toast 带进度条与进入/离开动画 |
| 表格 | `.table-shell` | 表头 surface-2 + muted 小字；行 hover surface-2/60 |
| 标签栏 | `ScrollTabs`、`PillTabs` | 单行横滑、隐藏滚动条、snap 吸附、活动标签自动居中；PillTabs 依赖 gsap，按需引入 |
| 概览网格 | `MagicBento` | 深色 Bento 卡 + 光标聚光；依赖 gsap，按需引入；移动端与 reduced-motion 下自动静置 |
| 氛围层 | `FloatingBackground` + `useFloatingBackground` | 纯 Canvas 复合运动（水平漂移 + 垂直正弦），无第三方依赖 |
| 主题切换 | `ThemeToggle`、`useTheme` | 存储键来自槽位 17；首帧前内联脚本应用 `html.dark` |
| 反馈微件 | `AnimatedNumber`、`PageSkeleton`、`shimmer`、`.spinner`、`.btn-ripple` | 入场 150–350ms；骨架扫光用 `background-position` |

**移植纪律**：只移植需要的组件；带 gsap 的组件（PillTabs/MagicBento/StrokeText）确认体积与 CSP 约束后再引入；生产环境 `style-src 'self'`（无 `unsafe-inline`），动效必须尊重 `prefers-reduced-motion`。

---

## 6. 验收清单（Pre-Delivery Checklist）

- [ ] 无 emoji 充当图标（统一 SVG）
- [ ] 图标来自一致图标集（Heroicons/Lucide/内置 SVG）
- [ ] 所有可点击元素有 `cursor-pointer`
- [ ] hover 状态有 150–300ms 平滑过渡
- [ ] 浅色模式正文对比度 ≥ 4.5:1
- [ ] 键盘焦点可见（`focus-visible` 2px 主色描边）
- [ ] `prefers-reduced-motion` 已尊重
- [ ] 响应式：375px / 768px / 1024px / 1440px 四档
- [ ] 无内容被固定导航遮挡
- [ ] 移动端无横向滚动
- [ ] 令牌无硬编码 hex（组件内），文案无硬编码（从 `brand.ts` 读取）
- [ ] 明暗模式切换无闪烁、无对比度丢失

**动效专项验收**：

- [ ] 所有飘动元素 `animation-iteration-count: infinite`
- [ ] 各页元素数量与 4.3 浓度分层一致
- [ ] `animation-delay` 已错峰，无两个元素同时从同侧进入
- [ ] 表单聚焦时循环速度减半、列表页滚动联动（0.5x–1.5x）
- [ ] 表格/核心阅读区无循环元素侵入
- [ ] 移动端（<768px）元素数 ≤ 6
- [ ] `prefers-reduced-motion` 下循环静止为单帧
- [ ] Chrome Performance 录制 60s：无 Layout Shift，GPU 内存稳定

---

## 7. 治理与演进规则

- **变更流程**：新视觉决策先写 BRAND.md（意图 + 理由）→ 再在 `index.css` 以令牌落地 → 复用既有组件模式 → 对照本文档差距自查。
- **允许偏离的情形**：主色因产品域调整（走 3.1 取色方法）；符号隐喻重映射；确需新模式时先写 spec 再更新 MASTER.md 页面模式清单。
- **禁止偏离的情形**：五大原则、动效铁律、单一事实来源分层、无障碍/节能底线。
- **漂移治理**：任何 PR 涉及视觉，对照第 6 章清单与项目 BRAND.md 差距表自查；代码与文档冲突时以代码为事实，并回写文档。

---

## 8. 多 Agents 协作方法（首次设计）

首次设计建议按多 Agents 协作执行：root agent 负责拆解、指派与验收，sub-agents 各执行一个有明确边界、可独立验证的 Task。本节把第 3–6 章的「填槽位 → 复制令牌 → 搭外壳 → 过验收」映射为**可并行、零文件重叠**的任务单元；日常开发期的协作规范由各项目自己的 `AGENTS.md` 承载（模板见本仓库 [AGENTS.md](AGENTS.md)）。

**总原则**：单一事实来源、一个任务一个 owner、并行任务零文件重叠。

### 8.1 角色与职责

| 角色 | 职责 |
| --- | --- |
| root agent（设计 owner） | 读本方案 → 拆解 Task → 指派 → 收集验证证据 → 向用户交付；槽位中需人拍板的决策（定位、主色、氛围浓度等）汇总后询问用户，禁止用猜测代替调查 |
| sub-agent（Task owner） | 只执行被指派的 Task，交付可验证证据；不越权扩张，任务含糊先澄清再动手 |

### 8.2 任务分解与文件所有权

| Task | 内容 | 产出文件 | 依赖 | 验收证据 |
| --- | --- | --- | --- | --- |
| T1 填槽位 | 第 3 章槽位 1–20 | `design-system/<project>/BRAND.md` | 本方案 | 20 项齐全、每项有决策理由 |
| T2 令牌落地 | 第 4.1 节、槽位 7–12/16 | `frontend/src/index.css` | T1 | 无 `{{PROJECT_PREFIX}}` 残留、明暗两套齐全 |
| T3 品牌单点 | 槽位 1/3/18、3.2 资产规则 | `frontend/src/lib/brand.ts` | T1 | 品牌文案仅存在于该文件 |
| T4 浏览器品牌位 | 槽位 16/17/20 | `frontend/index.html` | T1、T3 | favicon / theme-color / description / 首帧主题脚本齐全 |
| T5 组件与页面外壳 | 第 5 章、4.3 节 | `frontend/src/components/`、`frontend/src/pages/` | T2 | 组件无硬编码 hex/文案，外壳符合 4.3 |
| T6 氛围层与主题 | 2.4 节、槽位 17/19 | `FloatingBackground` 接入 + `useTheme` | T2 | 浓度分层正确、reduced-motion 收敛单帧 |
| T7 验收 | 第 6 章 | `design-system/<project>/MASTER.md`、`preview/` 截图 | 全部 | 清单全勾 + 对比度数值 + 截图 |

**并行规则**：T2/T3/T4 依赖 T1，先 T1 后并行 T2–T4；T5/T6 依赖 T2，可并行；T7 最后串行。任意时刻每个文件只有一个 owner；需要改他人文件先认领并经 root 同意；并行数量不超过可用并发槽位。T5 与 T6 同处组件目录，须按组件类名细分所有权，确保不编辑同一文件。

> 前端结构与默认假设不同时（如 Li&Chat 当前为 `static/` 原生静态页），T2–T6 的文件路径按项目实际结构映射，令牌落地为项目实际样式文件；映射方式先在 T1 的 BRAND.md 中写明。

### 8.3 派活与执行纪律

- Task 必须写清 **Consumes**（读哪些事实与文件）与 **Produces**（产出精确到文件 + 对外契约），验收标准可独立验证；写法可参考项目 `docs/superpowers/plans/` 的任务卡惯例。
- 动手前先读本方案对应章节与项目 `AGENTS.md`；不确定就问 root，不许用猜测代替调查。
- 验证才算完成：给出第 6 章清单证据（截图、对比度、占位符检查、四档响应式），失败说明原因与证据。
- 不做破坏性操作；不动他人未提交的改动；子 agent 不自行切分支或合并 main。

### 8.4 评审与验收

- **两段评审**：① 规范符合性——第 2 章内核、第 3 章槽位、第 6 章清单；② 质量门禁——占位符清零、无硬编码、WCAG 对比度（正文 ≥ 4.5:1）、`prefers-reduced-motion`、四档响应式。
- root 只依据**验证输出**验收，不接受无证据的「完成」。
- **冲突裁决**：`index.css` / `brand.ts` 是运行时事实，文档与代码冲突以代码为准并回写文档；agent 间分歧由 root 用可复现事实裁决；品牌方向分歧停下询问用户。

### 8.5 派活示例（Li&Chat 首次设计）

1. T1 → 子 agent A：填槽位，Consumes 本方案第 2–3 章，Produces `design-system/chat/BRAND.md`。
2. T2–T4 → 并行：agent B `frontend/src/index.css`、agent C `frontend/src/lib/brand.ts`、agent D `frontend/index.html`（Consumes T1 的槽位决策，产出文件互不重叠）。
3. T5–T6 → 并行：agent E 组件与页面外壳、agent F 氛围层与主题（Consumes T2 令牌；按组件类名划分所有权）。
4. T7 → 验收 agent G：跑第 6 章清单，产出 `MASTER.md` 与 `preview/` 截图，root 复核后交付。

---

## 附录 A：事实来源映射（本次提取的可追溯清单）

> 表中「参考实现」指首个实例化项目 Li&Pass 的同名文档（BRAND.md / MASTER.md / index.css / brand.ts / index.html），仅作来源注明；本仓库不包含、也不依赖这些外部文件。

| 提取内容 | 来源 |
| --- | --- |
| 定位、人格、承诺、避免清单 | `参考实现 BRAND.md` §1 |
| 五大原则 | `参考实现 BRAND.md` §2 |
| 色彩系统、字体、形状间距、Logo 图标 | `参考实现 BRAND.md` §3 |
| 四模式动效、错峰、联动、移动端降级 | `参考实现 BRAND.md` §4 |
| 页面品牌应用、文案语调、治理 | `参考实现 BRAND.md` §5–7 |
| 组件规格、页面模式、反模式、交付清单 | `参考实现 MASTER.md` 全文 |
| 令牌实际值（浅/深）、阴影、缓动、组件类 | `参考实现 index.css` |
| 品牌名、slogan、Logo、备案槽位 | `参考实现 brand.ts` |
| 浏览器品牌位、首帧主题脚本 | `参考实现 index.html` |
| 氛围层 Canvas 接入参数 | `参考实现 MASTER.md` §FloatingBackground + `参考实现 ambient-background-design 规格` |

## 附录 B：Li&Pass 令牌快照（供对照与回滚）

浅色模式（`:root`）：

| 角色 | 值 |
| --- | --- |
| bg / surface / surface-2 | `#F8FAFC` / `#FFFFFF` / `#F1F5F9` |
| fg / muted / border | `#0F172A` / `#64748B` / `#E2E8F0` |
| primary / hover / soft / fg | `#0369A1` / `#075985` / `#E0F2FE` / `#FFFFFF` |
| success / warning / destructive | `#15803D` / `#B45309` / `#DC2626` |
| ring | `#0369A1` |

深色模式（`.dark`）：

| 角色 | 值 |
| --- | --- |
| bg / surface / surface-2 | `#0B1220` / `#111A2C` / `#1B2740` |
| fg / muted / border | `#E2E8F0` / `#94A3B8` / `#263449` |
| primary / hover / soft / fg | `#38BDF8` / `#7DD3FC` / `rgba(56,189,248,0.14)` / `#082F49` |
| success / warning / destructive | `#4ADE80` / `#FBBF24` / `#F87171` |
| ring | `#38BDF8` |

阴影与动效：`--shadow-sm/md/lg` 三档弥散阴影（透明度总和 < 0.1）；`--ease-out`（入场）、`--ease-spring`（按压/弹窗）；`--motion-fast/base/slow = 150/250/350ms`。

## 附录 C：规则库交叉验证结论

本方案的通用标准与 ui-ux-pro-max 规则库交叉验证（2026-08-16 检索）：

- **color / `trust security corporate blue`**：首位结果（Insurance Platform）主色 `#0369A1`、Ring `#0369A1`、Destructive `#DC2626`，与 Li&Pass 主色一致；Notes 明确「Security blue + protected green [Accent adjusted for WCAG 3:1]」。
- **typography / `corporate trust professional`**：首位「Corporate Trust」组合 Lexend（标题）+ Source Sans 3（正文），Notes「Lexend designed for readability. Excellent accessibility.」——与参考实现 BRAND.md §3.2 的自托管建议一致，正文保持系统字体栈 + 中文回退。
- **ux / `reduced motion accessibility performance`**：三条均 Severity High——必须检查 `prefers-reduced-motion`、避免强制滚动特效、每个视图最多动画 1–2 个关键元素。与本方案 2.4 铁律一致。
- Li&Pass 设计时已验证：`--design-system "sso identity authentication security trust enterprise portal"` 输出「Enterprise Gateway / Trust & Authority」模式，主色同为 `#0369A1`（见参考实现 BRAND.md 附录）。

## 附录 D：实例化样例与后续建议

- **首个实例化样例**：Li&Pass。本方案按其提炼；其项目内已具备 `design-system/<project>/BRAND.md` 与 `MASTER.md`，符合 §1.2 的要求。
- **视觉对齐参照**：各项目把页面截图/预览保存在各自 `design-system/<project>/preview/`，作为项目内对照基准；本仓库不提供外部图片引用。
