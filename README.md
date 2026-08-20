# Li&Design · 可复用设计模板

> ⚠️ **使用边界：本仓库仅在项目第一次设计时参考。** 每个项目必须在自己的仓库中生成适用于当前项目的设计方案（`design-system/<project>/BRAND.md` + `MASTER.md` 与落地令牌）。首次设计完成后，后续开发一律以项目内方案为准，不再依赖本仓库。

Li& 系列产品的共用品牌/视觉设计模板仓库：从 Li&Pass 已验证的设计系统提炼，供所有子项目（Li&Chat 及后续新项目）按「填槽位 → 复制令牌 → 过验收」的方式实例化。

> **V1.4（2026-08-20）**：完成全家族（About / Pass / Chat / Blog / Panel）视觉实现总览；采纳 AA 调校语义色、深色软底实色粉彩、极光/科技光效完整 CSS、零依赖等价实现，并补全下拉/菜单/头像/复选/文件/分页/面包屑/进度等全部 UI 控件，确保新项目可 1:1 复刻；新增**防跨项目复制**硬规则。

## 目录结构

| 文件 | 用途 |
| --- | --- |
| [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md) | **全家族实现总览**：项目矩阵、已验证参数、效果对照表、防复制治理；新项目先读此文件 |
| [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) | 主方案：品牌内核（不变层）+ 项目适配槽位表（22 项）+ 落地流程 + 组件库 + 验收清单 + 多 Agents 协作方法（第 8 章） |
| [reusable-tokens.template.css](reusable-tokens.template.css) | Tailwind CSS 4 令牌骨架，含 `{{PROJECT_PREFIX}}` 占位符、明暗两套色板、极光/科技光效与完整组件 CSS（含下拉/菜单/头像/复选/文件/分页/面包屑/进度） |
| [reusable-readme.template.md](reusable-readme.template.md) | 可复用 README 模板：结构约定 + 徽章规则 + 写作原则，含占位符与使用说明 |
| [AGENTS.md](AGENTS.md) | 模板仓库的多 Agents 协作手册：事实来源、硬性规则、协作规范、验证命令 |

## 快速上手（新项目 3 步）

1. 先读 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md) 确认家族现状，再复制 `reusable-tokens.template.css` 到新项目 `frontend/src/index.css`，把 `{{PROJECT_PREFIX}}` 换成项目技术标识（如 `lipass`、`chat`），按槽位表填色值。
2. 按 [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) 第 3 章逐项填写适配槽位（名称、定位、主色、语义色、字体、Logo、氛围浓度等）。
3. 按第 4 章搭建组件与页面外壳，最后过第 6 章 Pre-Delivery Checklist；多 Agents 协作实例化见第 8 章。**禁止从任何项目仓库复制文件。**

## README 模板（Li&About 规范）

由 Li&About 个人主页沉淀的可复用 README 结构，适用于项目主页与个人主页。

### 用法（3 步）

1. 复制 `reusable-readme.template.md` 到新项目根目录，改名 `README.md`
2. 替换全部 `{{PLACEHOLDER}}` 占位符
3. 删除不适用的小节与注释块，不留空占位符

### 结构约定

| 板块 | 说明 |
| --- | --- |
| 标题 + 一句话定位 | `# 项目 · 仓库` + `> tagline` |
| 顶部徽章 | 状态/角色/方向 + 技术徽章（平铺不分组） |
| 目录 | README 较长时启用，锚点与标题一致 |
| 关于 | 1–2 段介绍 + 关键信息表 |
| 技能栈 | 徽章平铺 + 领域详情表 |
| 项目 | 项目/简介/技术栈/状态四列表 |
| 当前目标 | 目标/说明/期限表 |
| 路线图 | 近期/中期/远期 |
| 仓库结构 | text 代码块目录树 |
| 许可 | `© 年份 作者` |

### 徽章规则

- 状态/角色/方向徽章：shields.io 默认样式（如 `status-active-brightgreen`）
- 技术徽章：shields.io 默认 flat 样式 + `logo=<simple-icons slug>` + 官方品牌色，并链接到技术官网
- 格式：`[![TECH](https://img.shields.io/badge/TECH-COLOR?logo=SLUG&logoColor=white)](OFFICIAL_URL)`
- 技术徽章平铺排列，不按类别分组
- 常用品牌色：Linux `FCC624`、Docker `2496ED`、Kubernetes `326CE5`、Python `3776AB`、FastAPI `009688`、React `61DAFB`（黑字）、TypeScript `3178C6`、PostgreSQL `4169E1`、Redis `DC382D`、Tailwind CSS `06B6D4`、Markdown `000000`
- simple-icons 无对应 logo 的技术（如 WebSocket、WebRTC）用纯文字徽章

### 写作原则

- 只写真实信息，不编造熟练度、数据或链接
- 只列实际掌握的技术；借助 AI 构建项目时用到的技术不列入技能徽章
- 详细数据放独立文件（如 profile.md），README 只引用，保持单一事实来源
- 没有对应内容就删除该小节，不留 TBD/TODO
- 托管项目链托管地址，未托管用相对路径
- 技术名保持官方大小写：FastAPI、TypeScript、PostgreSQL、Kubernetes、Tailwind CSS、WebRTC
- 表情克制，技术类 README 每 3–5 段最多 1 个表情

## 首次设计必交产出（在项目内生成）

| 产出物 | 位置 | 说明 |
| --- | --- | --- |
| 项目品牌方案 | `design-system/<project>/BRAND.md` | 品牌内核 + 已填槽位的项目版 |
| 实现速览 | `design-system/<project>/MASTER.md` | 令牌、组件、页面模式快照 |
| 令牌落地 | `frontend/src/index.css` | 复制模板、换前缀、填色值 |
| 品牌单点 | `frontend/src/lib/brand.ts` | 名称 / slogan / Logo / 备案 |
| 项目协作手册 | `AGENTS.md`（项目根） | 参照模板仓库 [AGENTS.md](AGENTS.md) 与方案第 8 章 |

## 核心原则（速记）

- 信任优先、克制科技感、以动衬静、单一事实来源、无障碍节能。
- 60/30/10 用色比例；深色 = 去饱和浅色调变体（可选「雾灰中间调」不压黑）；主色永远小面积强调。
- V1.2 海玻璃示例：全淡色、无粉色、无重色；主按钮半透明着色；六强调色板 + 科技光效层（网格/光束/光点）。
- V1.3：浅色语义色用 AA 调校值（muted `#64736C` / success `#2A7C52` / warning `#9A5C05` / destructive `#C43737`）；深色带文字软底用 `*-soft-solid` + `*-soft-fg`。
- V1.4：UI 控件全量内置——`.select`（原生下拉同输入框视觉）、`.custom-select-*`（键盘完整自定义下拉）、`.dropdown-menu`、`.suggest-menu`、`.avatar`、复选/文件按钮、`.pagination`、`.breadcrumb`、`.progress`、`.table-empty-row`。
- 动效只动 `transform/opacity/background-position`，每个 animation 必须有 @keyframes，尊重 `prefers-reduced-motion`，移动端减量省电。
- 令牌只存在 `index.css`，品牌文案只存在 `brand.ts`，组件禁止硬编码。
- 新效果/新调校先回写本模板再引用；禁止项目间复制（详见实现总览 §5）。
- 多 Agents 协作：单一事实来源、一个任务一个 owner、并行任务零文件重叠（方案第 8 章 + [AGENTS.md](AGENTS.md)）。

## 参考实现

本仓库内容自包含，不依赖任何相邻目录或外部链接；文中引用的 Li&Pass 令牌与槽位示例已内联在文档中，克隆到任意位置均可直接使用。

## 治理

- 新视觉决策先写 BRAND.md 意图，再以令牌落地；代码事实与文档冲突时以代码为准并回写文档。
- 示例取值来自全家族已验证实现（Li&Pass 历史快照见方案附录 B.1；V1.3 调校值见 B.2）；新项目按第 3 章填自己的槽位，不引用外部仓库。
- 本仓库只承载模板的演进；各项目的设计方案在各自仓库内独立演进。
- 多 Agents 协作遵循 [AGENTS.md](AGENTS.md) 与方案第 8 章：并行任务零文件重叠，root agent 只按验证输出验收。
