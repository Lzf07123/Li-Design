# Li& 系列项目视觉实现总览（Implementation Index）

> **版本**：V1.4 ｜ **日期**：2026-08-20 ｜ **状态**：全家族审计结果（Li&About / Li&Pass / Li&Chat / Li&Blog / Li&Panel；V1.4 补全选择/下拉/菜单/头像/复选/文件/分页/面包屑/进度等 UI 控件）
> **用途**：这是「谁实现了什么、参数是什么、差异在哪」的唯一入口。新项目实例化前先读本文件 + [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) 第 2–3 章，再从 [reusable-tokens.template.css](reusable-tokens.template.css) 复制落地，**禁止从任何项目仓库复制文件**。
> **事实来源**：各项目 `design-system/<project>/BRAND.md`、`MASTER.md` 与落地代码（`index.css` / `style.css` / `tokens.css` / 组件源码），以代码事实为准。

---

## 1. 项目矩阵

| 项目 | 前端形态 | 令牌前缀 | 方案版本 | 实例化状态 | 视觉实现要点 |
| --- | --- | --- | --- | --- | --- |
| Li&About | Markdown 个人主页（无前端代码） | — | README 规范 | 已沉淀为 [reusable-readme.template.md](reusable-readme.template.md) | 徽章平铺规则、官方品牌色、写作原则、结构约定 |
| Li&Pass | React + Tailwind CSS 4（motion/react + gsap 按需） | `portal` | BRAND V2.0 / 2026-08-17 | **参考实现本体**（V1.2 模板提取来源） | AuthShell / AppHeader / PillTabs / MagicBento / StrokeText / BlurText / CountUp / FloatingBackground / AuroraBackground / TechAmbience（网格 + 3 光束 + 8 光点）/ card-signature / flow-rule / card-halo / toast / modal / table-shell / 半透明按钮 + 扫光；**原生 `<select className="input-sm">`（无自定义下拉）** |
| Li&Chat | 原生静态 HTML/CSS/JS（**零第三方依赖**） | `chat` | BRAND/MASTER V1.2 / 2026-08-17 | 模板 V1.2 全量采纳 + RGB 调校 | 语义色调校（AA 达标）、深色软底 soft-solid/soft-fg、零依赖 BlurText/CountUp/ripple/card-signature/flow-line、微信式双栏应用外壳、status-dot、紧凑密度、消息气泡/多选/投票/表情/上传/图片查看器；**profile-dropdown 个人菜单、mention-list 建议选项、avatar 头像** |
| Li&Blog | Hugo + React/motion 效果层（esbuild 单文件，约 90KB gzip） | `liblog` | BRAND/MASTER v1.0 / 2026-08-18 | 模板 V1.2 实例化 + 调校值 + 站点化扩展 | 公开站零交互、本地徽章（无 shields.io 外链）、HeroFX 滚动视差、AuroraBackground full/soft = 4/2、TechAmbience 去光束（网格 + 8 枚强调色光点）、打印令牌、代码高亮令牌、文章页零动效、后台完整组件集（table-shell / **custom-select 键盘完整下拉** / upload-progress / checkbox+file 令牌化 / pagination / breadcrumb / toast / modal 等） |
| Li&Panel | React + Tailwind CSS 4 | `portal`（1:1 复刻）+ `lipanel` | BRAND/MASTER 2026-08-20 | **跨项目 1:1 复制（反例，需纠正）** | 与 Li&Pass 逐字一致（`--portal-*`、组件、动效、CSP）；面板网格 1→2→3→4 列；`site_settings` 品牌信息后台可覆盖；原生 select 同 Pass |

## 2. 家族共性（全部项目已验证）

### 2.1 已形成一致的内核

- 海玻璃主色 `#25786D`（浅）/ `#7FD4C6`（深），全淡色系、无粉色、无大面积重色；D1 雾灰深色中间调（不压黑）。
- 60/30/10 用色比例；主色永远小面积强调；语义色只表达状态。
- 主按钮半透明单色着色（浅 `rgba(47,127,116,.10)` / 深 `rgba(127,212,198,.13)`）+ 细描边 + `::after` 扫光；hover 上移 1px，按压 `scale(0.97)`。
- 三档水绿 tint 弥散阴影（透明度总和 < 0.1）；缓动 `--ease-out` / `--ease-spring`；时长 150/250/350ms。
- TRUST 五原则、呼吸感四模式（水平穿行 / 往复钟摆 / 正弦波形 / 盘旋公转）、科技光效层、极光层、卡片签名描边、流光线、文字浮现、数字滚动、焦点环、`prefers-reduced-motion` 单帧、移动端减量、SVG 图标（禁 emoji）。
- 单一事实来源：令牌只在 CSS 事实文件，品牌文案只在 brand 单点（`brand.ts` / `brand.js` / `config/brand.yaml`）。
- 表单与选择控件完整：原生 select 与输入框同视觉（V1.4 `.select`）；自定义下拉、下拉菜单、建议选项、头像、复选框/单选/文件按钮、分页、面包屑、进度条、空状态均有模板实现（§3 对照表）。

### 2.2 语义色 AA 调校结论（V1.3 模板默认采用调校值）

Li&Chat 按模板附录 E 方法对浅色语义色做同色相加深，Li&Blog 已采纳；Li&Pass / Li&Panel 仍为模板旧值。WCAG 对比度（底色 `#F6FBF9`）实测：

| 角色 | 模板旧值 | 对比度 | 调校值（V1.3 默认） | 对比度 |
| --- | --- | --- | --- | --- |
| muted | `#71807A` | 3.96 ❌ | `#64736C` | 4.77 ✅ |
| success | `#2F8F5F` | 3.85 ❌ | `#2A7C52` | 4.89 ✅ |
| warning | `#A16207` | 4.71 ✅ | `#9A5C05` | 5.14 ✅ |
| destructive | `#CF3D3D` | 4.58 ✅ | `#C43737` | 5.09 ✅ |

> 结论：模板 V1.3 起，浅色语义色默认使用调校值；存量项目（Li&Pass / Li&Panel）属历史差异，后续做无障碍审计时按调校值对齐。

### 2.3 深色软底规则（Chat / Blog 已验证）

`rgba(浅色, 0.14–0.18)` 软底上的同色浅字对比上限 ≈ 3.9，达不到 4.5。带文字的软底组件必须用实色粉彩底 + 深字：

| 角色 | soft-solid（实色粉彩底） | soft-fg（深字） | 对比度 |
| --- | --- | --- | --- |
| primary | `#D9F4EE` | `#17332E` | 高（>10） |
| success | `#E3F6E9` | `#14532D` | 8.08 ✅ |
| warning | `#FDF3D8` | `#78350F` | 8.20 ✅ |
| destructive | `#FDEEEE` | `#7F1D1D` | 8.89 ✅ |

落地方式：CSS 引用 `var(--<prefix>-success-soft-solid, var(--<prefix>-success-soft))` 与 `var(--<prefix>-success-soft-fg, var(--<prefix>-success))`，带文字的组件自动回退；图标/图形可继续用 rgba 软底。

## 3. 效果对照表（「一模一样」的落地位置）

| 效果 | 模板位置（V1.4） | Li&Pass | Li&Chat | Li&Blog |
| --- | --- | --- | --- | --- |
| 海玻璃令牌（明暗两套） | `reusable-tokens.template.css` `:root` / `.dark` | `frontend/src/index.css` | `static/style.css` | `themes/blog-theme/static/css/tokens.css` |
| 主按钮半透明着色 + 扫光 | `.btn-primary` + `::after`（`btn-sheen` 4s） | 同模板 | `.btn-primary::after`（`chat-btn-sweep` 4s） | 后台同模板；首页 CTA 用 `--liblog-btn-light/dark-*` |
| 按钮涟漪 | `.btn-ripple`（500ms，JS 注入 span） | 组件 `AsyncButton` | `.btn-ripple` + `chat-btn-ripple` | 未接（后台按钮无涟漪） |
| 认证卡签名描边 | `.card-signature`（mask 环 + `flow-gradient` 9s） | `.card-signature`（双背景 border-box） | `.card-signature::after`（mask 环 9s） | 未接（后台无认证卡） |
| 卡片辉光 / Logo 辉光 | `.card-halo` / `.brand-halo`（4.5s） | `.card-halo` / `.brand-halo` | `.auth-halo` / `.auth-brand::before` | 未接 |
| 流光线 | `.flow-rule`（5s，`flow-gradient` 250% 位移） | `.flow-rule`（顶栏/分区标题） | `.flow-line`（顶栏底部，200% 位移） | 未接 |
| 极光层 | `.aurora` / `.aurora-blob`（4 枚，18/22/28/24s）+ `.aurora-soft` | `AuroraBackground` 4 枚 | 同模板（登录后 `.aurora-soft`） | `AuroraBackground` full=4 / soft=2 |
| 科技光效层 | `.tech-ambience` / `.tech-grid` / `.tech-beam` ×3 / `.tech-dot` ×8（12s / 10s 错峰 0.8/4.2/7.5s / 6s） | 同模板 | 同模板（`.tech-soft` 0.55） | 去光束：网格 + 8 枚强调色光点（`--tech-dot-color` 取六强调色） |
| 文字浮现 | `.blur-unit`（450ms、35ms 错峰；零依赖） | `BlurText`（motion/react，按词） | `.blur-unit`（零依赖） | `BlurText`（motion/react，IntersectionObserver） |
| 数字滚动 | 模板提供参数（`motion` 弹簧 damping=20+40/duration、stiffness=100/duration）；零依赖变体见附录 F | `CountUp`（motion/react） | `countUp` 三次缓动 450ms（零依赖） | `CountUp`（motion/react 弹簧） |
| 滚动视差 Hero | §2.4.2（scale 1→0.82、y −30px、opacity 1→0.35、blur 0→5px） | 未接 | 未接 | `HeroFX`（motion/react `useScroll` + spring） |
| 主题切换 + 首帧防闪烁 | 槽位 17 + 内联脚本；`html.dark` | `useTheme` + `portal-theme` | `theme.js` + `chat-theme` | 后台 `admin-theme-toggle` + `liblog-theme`（公开站跟随系统） |
| 浏览器品牌位 | §4.1 槽位 20 | `frontend/index.html` | `static/index.html` | Hugo head 模板 |
| Toast / Modal | `.toast-*`（z-80）/ `.modal-*`（z-70） | 同模板 | `.toast` 安全区置顶 | 后台同模板 |
| 表格 | `.table-shell`（表头 surface-2 + muted 小字；移动端横滑） | 同模板 | 未接 | `admin/templates/partials/table.html`（50 轮迭代） |
| 原生下拉 | `.select` / `.select-sm`（双三角渐变 chevron，与 `.input` 同视觉） | `<select className="input-sm">` | 未用（无筛选场景） | `.list-filters select`（36px 等高） |
| 自定义下拉 | `.custom-select-*`（button + listbox，键盘完整，零依赖） | — | — | `admin-dropdown.js` + `.custom-select-*` |
| 下拉菜单 | `.dropdown-menu` / `.menu-item` / `.menu-item-danger` | — | `.profile-dropdown` / `.profile-menu-item` | — |
| 建议选项 | `.suggest-menu` / `.suggest-option`（胶囊 chips） | — | `.mention-list` / `.mention-option` | — |
| 头像 | `.avatar` / `.avatar-placeholder`（28/32/36/56px） | 组件头像（品牌单点） | `.avatar` / `.avatar-placeholder` | `.table-thumb`（64×48 封面缩略） |
| 选择控件 / 文件按钮 | checkbox/radio 18px `accent-color` + `.field-check` + `file-selector-button` | — | 消息多选 `.select-bar` | `admin.css` 令牌化复选 + 文件按钮 |
| 分页 / 面包屑 | `.pagination` / `.breadcrumb` | — | — | `.pagination` / `.admin-breadcrumb` |
| 进度条 / 空状态 | `.progress` / `.table-empty-row` | `.toast-progress` | `.upload-progress-*` | `.upload-progress` + `.table-empty-row` |
| 本地徽章（公开站） | §5 `badge` 行（本地 SVG 胶囊，零外链） | — | — | `themes/blog-theme` badge 组件 |
| 打印 / 代码高亮令牌 | §3.1 可选扩展（`--print-*` / `--code-*`） | — | — | `tokens.css`（白纸黑字 + Chroma 六色） |
| 应用外壳 | AuthShell（`max-w-md` 居中卡）；AppShell = AppHeader + `max-w-7xl` + Footer | 同模板 | 微信式双栏（列表 300px + 内容 ≤880px；`100dvh` 内滚） | 公开站无交互外壳 + 后台管理外壳 |
| 页脚 | `.site-footer` / `.site-footer-inner` / `.filing-icon-placeholder`（`mt-auto` 贴底 + 半透明表面 + backdrop-blur；版权/备案/链接全部由 brand.ts 驱动） | `SiteFooter.tsx`（brand.ts 静态，Pass 已验证） | Chat 自有 `.site-footer`（`static/style.css`） | 公开站自有 `footer.site-footer` / `.footer-inner`（备案 + CC 协议） |

## 4. 各项目独有模式（按需引用，不是默认内核）

### 4.1 Li&Chat：零依赖实现清单（不加载远程资源的等价方案）

模板提及的 motion/gsap 组件，Chat 全部以原生 CSS/JS 等价实现：

| 模板效果 | 零依赖等价实现 | 参数 |
| --- | --- | --- |
| BlurText | `.blur-unit` 词级拆分 + `--blur-index` | 450ms、35ms 错峰、blur 8px、y 6px |
| CountUp | `countUp` 三次缓动 | 450ms，未读/申请/归档徽章变化时触发 |
| 按钮涟漪 | `.btn-ripple` span + `animationend` 移除 | 500ms，currentColor |
| 签名描边 | `.card-signature::after` mask 环 | 9s 无缝循环 |
| 流光线 | `.flow-line` | 5s、200% 背景位 |

### 4.2 Li&Blog：内容站点扩展

- **HeroFX 滚动视差**：`scale` 1→0.82、`y` −30px、`opacity` 1→0.35、`blur` 0→5px，按首屏滚动进度映射；`prefers-reduced-motion` 渲染静态。
- **氛围分级**：`data-ambient` = `full`（首页 8 形状 + 4 极光 + 网格光点）/ `soft`（4 形状 + 2 极光 + 淡网格光点）/ 0（文章页零动效、不加载效果包）。
- **本地徽章**：公开站徽章 = 本地 SVG 胶囊（官方品牌色圆点/整块底 + 白字 + 本地图标），禁止 shields.io 外链；README 仍按 Li&About 规范用 shields.io。
- **打印令牌**：`--liblog-print-bg: #fff` / `--liblog-print-fg: #000`，白纸黑字不随主题。
- **代码高亮令牌**：comment / keyword / string / number / func / type / lineno 明暗两套，映射 Chroma。
- **自定义下拉契约**：`select[data-custom-dropdown]` 由 `admin-dropdown.js` 渐进增强为 button + listbox；隐藏原生 select 仍是表单事实源（选中后派发 `change`），键盘 ArrowUp/Down/Home/End/Enter/Space/Escape 与 `aria-expanded`/`aria-selected` 完整同步。模板 `.custom-select-*` CSS + 契约见方案附录 F。

### 4.3 Li&Panel：网格与后台品牌覆盖

- 面板网格响应式 1→2→3→4 列（375 / 768 / 1024 / 1440）。
- `brand.ts` 保存设计默认值，首次启动种子写入 `site_settings`；运行时以 `site_settings` 为事实来源，清空回退默认——可见品牌信息后台可改（含页脚：`SiteFooter site` 属性 + `APP_VERSION` / `footer_text`，备案图标缺失/加载失败时用 `.filing-icon-placeholder` 字形方块占位）。
- ⚠️ Panel 当前为 `--portal-*` 1:1 逐字复刻，模板更新无法传导。本仓库 V1.3 发布后，Panel 应改为从模板重实例化（仅槽位 1–6、16–18 不同）。

## 5. 防跨项目复制治理（新增硬规则）

1. 新项目**禁止**从 Li&Pass / Li&Chat / Li&Blog / Li&Panel 复制样式或组件文件；一律从 `reusable-tokens.template.css` + 本索引实例化。
2. 任何项目发现新效果、新调校或新组件模式：先在 Li&Design 更新模板（写意图 + 参数 + 验收证据），再在项目内引用；**不允许**先落项目、后补模板。
3. 实例化完成后做一次「仅槽位差」校验：`rg -o -- '--<prefix>-[a-z0-9-]+' <project>/<tokens-file> | sort -u` 与模板变量集合对比，除前缀外不允许结构性差异。
4. Li&Pass / Li&Chat / Li&Blog 的项目内 `design-system/<project>/` 方案继续独立演进；与模板冲突时以代码事实为准并回写模板，避免双源漂移。

## 6. 与 REUSABLE-BRAND-SCHEME.md 的关系

- 本文件回答「家族现状是什么」；方案文档回答「新项目应该怎么做」；令牌模板回答「代码长什么样」。
- 方案文档第 2–3 章（内核 + 槽位）不变；第 5 章组件库与附录 B/E/F 已按本索引更新到 V1.4。
