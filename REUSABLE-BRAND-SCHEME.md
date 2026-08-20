# Li& 系列 · 可复用品牌设计方案

> **版本**：V1.5 ｜ **日期**：2026-08-21 ｜ **状态**：可复用基准（V1.3 采纳 AA 调校语义色、深色软底实色粉彩、极光/科技光效完整 CSS、零依赖等价实现与防跨项目复制治理；V1.4 补全选择/下拉/菜单/头像/复选/文件/分页/面包屑/进度等全部 UI 控件，确保 1:1 复刻；V1.5 纳入 Pass/Panel 已验证页脚组件与备案图标占位）
> **存放位置**：独立模板仓库，可置于任意位置（与各子项目同级或克隆到其他机器），供所有子项目共用参考。
> **提取来源**：Li&About（README/徽章规范）、Li&Pass（参考实现本体）、Li&Chat（AA 调校 + 零依赖等价）、Li&Blog（站点化扩展 + HeroFX + 本地徽章）、Li&Panel（1:1 复刻反例）——全部提炼内联于本文档与 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md)，不依赖源仓库路径。
> **配套文件**：[PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md)（全家族实现总览：项目矩阵 / 效果对照表 / 防复制治理）、[reusable-tokens.template.css](reusable-tokens.template.css)（复制、改前缀、填色值后即可用）、[AGENTS.md](AGENTS.md)（模板仓库的多 Agents 协作手册，与第 8 章配合使用）。
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
- **家族实现总览**：先读 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md)，确认「谁已实现什么、参数是什么、差异在哪」，避免重复发明或跨项目复制。

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
2. **淡色科技感（Light-Toned Tech，V1.3 修订）**：中性或淡色底色 + 单一主色强调，**全淡色系、无粉色、无大面积重色**（家族定稿「海玻璃」主色 `#25786D`，浅色 600 档；`#2F7F74` 为早期推导中间值，已被代码事实取代）；按钮用半透明单色着色而非渐变色块；科技感来自雾面粉彩层次、网格/光束/光点的流动光效与动效质感。霓虹渐变、AI 紫粉、夸张玻璃拟态仍禁止。
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

#### 2.4.1 科技光效层（TechAmbience，V1.2 新增，可选变体）

在几何暗线之外，可选叠加一层**可见但克制**的科技光效，由三个纯 CSS 装饰组成（Li&Pass 定稿参数）：

| 元素 | 说明 | 节奏 |
| --- | --- | --- |
| 缓移网格 `.tech-grid` | 56px 基线 + 336px 亮线双层 repeating-gradient，径向渐隐遮罩，`background-position` 漂移（移动整数倍周期保证无缝循环） | 12s |
| 扫掠光束 `.tech-beam` | 斜切 16° 的透明渐变带，`translateX` 扫过并长停顿；多条错峰 | 10s（错峰 0.8/4.2/7.5s） |
| 呼吸光点 `.tech-dot` | 7px 圆点 + 辉光，`opacity/transform` 脉动并上下浮动 | 6s |

**铁律（补充）**：

- 光效层 `aria-hidden` + `pointer-events: none`；认证页默认浓度，工作台 `soft`，后台可接入 `soft`（表格区保持不透明表面，可读性优先）。
- **每个 `animation` 必须存在对应 `@keyframes`**——历史缺陷：只写 `animation` 引用、漏定义关键帧导致光束基态 `opacity:0` 且完全不运动、不可见；验收时逐一核对。
- 光效层只动 `transform/opacity/background-position`；`prefers-reduced-motion` 单帧；移动端隐藏光束/光点并停用网格动画。

典型参数区间（可在项目内微调，但保持「极慢极淡」的量级）：

| 元素 | 轨迹 | 单次周期 | 透明度 | 缩放 |
| --- | --- | --- | --- | --- |
| Z 形飘片（大） | A | 45s | 0.06–0.12 | 0.8–1.2 |
| Z 形飘片（小） | B | 30s | 0.10–0.18 | 0.5–0.8 |
| 正方飘块 | B | 40s | 0.06–0.10 | 0.6–1.0 |
| 圆点光斑 | D | 25s | 0.15–0.25 | 0.8–1.5 |
| 几何线条（长） | A | 60s | 0.04–0.08 | 1.0 |
| 锁钥组合 | C | 90s | 0.04–0.06 | 0.9–1.1 |

#### 2.4.2 极光层与滚动视差（V1.3 新增）

**极光层（AuroraBackground，V1.2 提及、V1.3 给出完整 CSS）**：4 枚 `radial-gradient` 弥散光斑（水绿/冰蓝/淡丁香/暖沙），无 `filter`、无阴影动画，只动 `transform`。参数：

| 参数 | 值 |
| --- | --- |
| 光斑数量 | 认证页 4；工作台/后台 `soft` 降为 2（Blog 已验证 full=4 / soft=2） |
| 漂移周期 | 18s / 22s / 28s / 24s（`alternate` 往返） |
| 光斑尺寸 | `min(46vw, 720px)` 圆斑，`closest-side` 径向渐变、72% 透明收尾 |
| 浓度令牌 | `--<prefix>-aurora-1..4`（明暗两套）；`.aurora-soft` 整体 opacity 0.55 |
| 移动端 | <768px 全层 opacity 0.7、单斑周期 52s |

**滚动视差（HeroFX，Blog 已验证，可选）**：Hero 区随页面滚动缓慢缩放/上移/淡出/柔焦，只对首屏高度做映射：

| 参数 | 值 |
| --- | --- |
| scale | 1 → 0.82（首屏滚动进度） |
| y | 0 → −30px |
| opacity | 1 → 0.35 |
| filter blur | 0 → 5px |
| 驱动 | `useScroll` + `useSpring`（stiffness 110 / damping 28 / mass 0.6）；仅动合成属性 |
| 无障碍 | `prefers-reduced-motion` 下渲染静态，不挂滚动监听 |

铁律：滚动视差不应用于阅读区；文章/长文页面禁用（Blog 文章页零动效）；只动合成属性（transform/opacity/filter 由 GPU 合成）。

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
| 7 | 主色（浅） | 主色 / hover / soft / fg 四件套 | `#25786D` / `#1F6359` / `#D9F4EE` / `#FFFFFF` |
| 8 | 主色（深） | 深色取雾面浅色调变体 | `#7FD4C6` / `#A5E4D9` / `rgba(127,212,198,0.16)` / `#17332E` |
| 9 | 中性色（浅） | bg / surface / surface-2 / fg / muted / border | `#F6FBF9` / `#FFFFFF` / `#EEF6F3` / `#35423F` / `#64736C` / `#E1ECE8`（muted 为 V1.3 AA 调校值） |
| 10 | 中性色（深） | 同序（D1 雾灰，不压黑） | `#3A3F45` / `#434950` / `#4B5259` / `#F0F2F4` / `#B8C0C7` / `#545C64` |
| 11 | 语义色（浅/深） | 成功 / 警告 / 危险，及 soft 底色；深色带文字组件配 soft-solid/soft-fg | 浅 `#2A7C52` / `#9A5C05` / `#C43737`（V1.3 AA 调校值）；深 `#86D6AC` / `#EAD48E` / `#E8A49A`；soft-solid/soft-fg 见附录 B |
| 12 | 焦点环 | 2px 主色描边 + 2px offset，`focus-visible` 全局生效 | 浅 `#25786D`，深 `#7FD4C6` |
| 13 | 字体栈 | 家族默认栈 + 中文回退；不加载远程字体 | Inter → 系统栈 → PingFang SC / 微软雅黑 |
| 14 | 可选标题字体 | 如需品牌辨识度，自托管（`font-display: swap` + subset），不做 CDN 引用 | Lexend（Corporate Trust 组合，仅页面标题） |
| 15 | Logo / favicon | 透明底 512×512 WebP 单格式；最小 32px；周围净空 ≥ 1/4 图标边 | `brand-logo.webp` / `favicon.webp` |
| 16 | 令牌前缀 | `index.css` 的 CSS 变量前缀，逐项目唯一 | `portal`（`--portal-bg` 等） |
| 17 | 主题存储键 | 首帧主题脚本与 `useTheme` 共用 | `portal-theme` |
| 18 | slogan / 备案 | 从 `brand.ts` 读取；备案上线前留空，禁止假占位号 | slogan + ICP/公安备案占位 |
| 19 | 氛围浓度 | 认证 / 授权 / 中心 / 后台的 shapeCount + 光效层 | 10 / 4 / 10 / 4（后台 opacity 0.5；光效层：认证默认、中心/后台 soft） |
| 20 | 浏览器品牌位 | favicon、`theme-color`（浅/深）、`description`、首帧主题脚本 | 见 `frontend/index.html` |
| 21 | 强调色板 | 六色相 strong/soft（浅/深各一套），稳定哈希分配 | ice `#2F678F`/aqua `#25786D`/lilac `#51488F`/sage `#557546`/mint `#2F7C52`/sand `#876741`（深色见附录 B） |
| 22 | 按钮与光效风格 | 按钮着色方式、深色明度、光效浓度基调 | 半透明单色按钮（浅 10% / 深 13% + 细描边）；深色雾灰中间调；光效「可见但克制」 |

### 3.1 取色方法

- 主色按产品域选择：用 ui-ux-pro-max 规则库 `--design-system "<product> <industry> <keywords>"` 检索推荐，再按 WCAG AA 校验前后景对比（正文 ≥ 4.5:1，UI 组件 ≥ 3:1）。
- **全淡色变体（Li&Pass 定稿口径）**：底色/表面保持浅色雾面，主色取该色相 700 档的雾面值（浅）/300 档（深）；**全站无粉色系、无大面积重色**；深色模式可用「雾灰中间调」（如 `#3A3F45`）替代近黑底，平均亮度显著提升。
- **强调色板**：六个低饱和色相（strong/soft 各一套）只做装饰性小面积（图标瓦片、图例、分区规则线、Bento 标签），合计 ≤ 15% 可视面积；strong-on-soft 文本对比 ≥ 4.5:1；实体 → 色相用稳定哈希，刷新不跳色。
- **按钮**：主按钮用半透明单色着色（浅 10% / 深 13% 透明度）+ 1px 同色细描边 + 深/浅文字，hover 只加深底色并抬升阴影；避免多色渐变色块造成的「违和感」。
- 用色比例约 **60/30/10**：中性色 ≈ 60%，表面内容 ≈ 30%，主色 + 语义色 ≈ 10%。主色永远是小面积强调，不做大面积主色背景。
- 语义色只表达状态，不用于装饰。
- **浅色语义色 AA 调校（V1.3 默认）**：模板旧值 muted `#71807A`（3.96）、success `#2F8F5F`（3.85）不达 4.5；同色相加深后 muted `#64736C`（4.77）、success `#2A7C52`（4.89）、warning `#9A5C05`（5.14）、destructive `#C43737`（5.09），全部 ≥4.5。新项目直接使用调校值，不再从旧值起步（实测数据见 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md) §2.2）。
- **深色软底规则（Chat/Blog 已验证）**：`rgba(浅色, 0.14–0.18)` 软底上的同色浅字对比上限 ≈ 3.9，达不到 4.5。带文字的软底组件（徽章/瓦片/提示条）必须回退到 `*-soft-solid`（实色粉彩底）+ `*-soft-fg`（深字）：primary `#D9F4EE`/`#17332E`、success `#E3F6E9`/`#14532D`、warning `#FDF3D8`/`#78350F`、destructive `#FDEEEE`/`#7F1D1D`（对比 8.0–8.9）。图标/图形可继续用 rgba 软底。
- 深色模式用**去饱和的浅色调变体**，不是简单反色；主色深色版取该色相 300–400 亮度档，soft 底色用 `rgba(主色, 0.12–0.18)`。
- **可选扩展（Blog 已验证）**：内容站点可加打印令牌（`--print-bg #FFFFFF` / `--print-fg #000000`，白纸黑字不随主题）与代码高亮令牌（comment/keyword/string/number/func/type/lineno 明暗两套，映射 Chroma）。
- 禁用清单：**粉色系（粉红/品红/玫瑰）**、大面积重色背景、霓虹渐变、纯黑 `#000`、低对比灰字、装饰性色块。低透明度的氛围点缀与卡片渐变描边除外（只出现在背景与描边层）。

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
| 控件尺寸 | 图标按钮 44×44px（移动端不缩小）；状态点 8px 圆点语义色；下拉触发器/分页按钮 min-height 36px，下拉菜单项 min-height 44px；桌面紧凑密度可收紧到按钮 30–36px、图标钮 34px（Chat 已验证，移动端仍保 44px 热区） |

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

1. **填槽位**：完整填写第 3 章槽位表（1–22 项），记录到 `design-system/<project>/BRAND.md`。
2. **铺令牌**：复制 `reusable-tokens.template.css` → `frontend/src/index.css`，替换前缀并填色值；`@theme` 只暴露语义别名（`bg-primary` 等），组件不直接引用 `--<prefix>-*`。
3. **建品牌单点**：按模板创建 `frontend/src/lib/brand.ts`，名称/slogan/Logo/备案全部从该文件读取。
4. **配浏览器品牌位**：`index.html` 配 favicon、明暗 `theme-color`、`description` 与首帧主题脚本（避免明暗闪烁），兜底背景色同步到令牌 bg。
5. **搭组件基座**：按第 5 章清单移植 `.btn` / `.card` / `.input` / `.badge` / `.notice` / `.modal` / `.toast` / `.table-shell` / `.site-footer` 等类；V1.3 模板已内置 `.card-signature` / `.card-halo` / `.flow-rule` / `.icon-btn` / `.status-dot` / `.scroll-tabs` / `.blur-unit` 与对应关键帧；可点击元素补 `cursor-pointer`。无远程资源项目用附录 F 零依赖等价实现。
6. **搭页面外壳**：认证类页用居中单卡 `AuthShell`（`max-w-md` + 顶部品牌 + slogan + 底部备案）；已登录页用 `AppHeader` + `max-w-7xl` 内容 + `SiteFooter`；管理类用顶部标签页。
7. **接氛围层**：复用 Canvas 版 `FloatingBackground`（无第三方依赖），按槽位 19 设 `shapeCount`/`opacity`/`calm`/`scrollWind`/`adaptive`/`theme="auto"`；画布 `z-0` 垫底、`pointer-events: none`。极光层（`.aurora`）与科技光效层（`.tech-grid`/`.tech-beam`/`.tech-dot`）的 CSS 与关键帧已随模板内置，按槽位 19 接 `.aurora-soft` / `.tech-ambience--soft` 降浓度。
8. **接主题**：`useTheme` 读写槽位 17 的存储键，切换 `html.dark`；所有明暗差异只通过 `.dark` 令牌块表达。
9. **过验收**：执行第 6 章 Pre-Delivery Checklist 与动效验收清单。
10. **回写治理**：把最终令牌、组件、页面模式回写 `MASTER.md`，变更理由回写 `BRAND.md`。

### 4.3 页面氛围浓度分层

| 页面类型 | 外壳 | 氛围浓度 | 关键约束 |
| --- | --- | --- | --- |
| 认证页（登录/注册/找回/验证等） | `AuthShell`：居中 `max-w-md` 卡片 + 极光背景 + 科技光效层 + 顶部品牌 + 底部备案 | 高（默认 10 + TechAmbience 默认） | 卡片及其上方 120px 禁飘；品牌名与 slogan 必须出现 |
| 授权/信任关键时刻 | `AuthShell` 变体 | 低（4） | 氛围减半；核心内容绝对清晰 |
| 用户中心/工作台 | `AppHeader` + `max-w-7xl` + `SiteFooter` | 中（10 + 滚动联动；极光/光效层 `soft`） | 卡片区域不遮字 |
| 管理后台 | `AppHeader` + 顶部标签页 | 低（4 × opacity 0.5；极光/光效层 `soft`） | 表格区域保持不透明表面，飘动元素不侵入表内文字 |

---

## 5. 组件与交互模式库（复用清单）

| 组件 | 类名 / 文件 | 复用要点 |
| --- | --- | --- |
| 按钮 | `.btn` 系列（primary/secondary/danger/ghost/link） | 主按钮半透明单色着色 + 细描边 + `::after` 扫光（4s，`--btn-sweep` 控制亮度）；`disabled` 时 `opacity-50` 且关闭扫光；点击涟漪 `.btn-ripple`（500ms，JS 注入 span） |
| 卡片 | `.card`、`.card-signature`、`.card-interactive` | 认证卡用 padding-box 表面 + border-box 低饱和品牌渐变描边双背景 |
| 认证卡辉光 | `.card-halo`、`.brand-halo` | 卡后浅主色呼吸辉光 + Logo 辉光，`isolation: isolate` 保证垫底 |
| 流光线 | `.flow-rule`（顶栏变体 `.flow-line`） | 分区标题短装饰线或顶栏底部全长渐变线，5s `background-position` 位移，`--flow-gradient` 明暗两套 |
| 表单 | `.label` / `.input` / `.input-sm` | focus 主色边框 + `ring-2 ring-primary/20`；placeholder 用 `text-muted` |
| 原生下拉 | `.select` / `.select-sm` | 与 `.input`/`.input-sm` 完全同视觉（Pass/Panel 用法）；令牌色 chevron 用双三角渐变绘制，不引入硬编码图标；`option` 走 surface/fg 令牌 |
| 自定义下拉 | `.custom-select-*` | Blog 已验证，渐进增强：隐藏原生 select + `button[aria-haspopup=listbox]` + `ul[role=listbox]` + `li[role=option]`；ArrowUp/Down/Home/End/Enter/Space/Escape、外点关闭、`aria-expanded` 同步；零依赖 JS 契约见附录 F |
| 徽章/提示条 | `.badge-*`、`.notice-*` | 语义色 + soft 底色；带状态图标；深色下带文字组件回退 `*-soft-solid` + `*-soft-fg`（实色粉彩底 + 深字），提示条正文用高亮浅色文字 |
| 图标按钮/状态点 | `.icon-btn`、`.status-dot` | 44×44px 热区 + 1.25rem SVG；8px 圆点表达 connecting/connected/disconnected/invalid |
| 下拉菜单 | `.dropdown-menu` / `.menu-item` / `.menu-item-danger` | Chat 已验证：触发器下方绝对定位，surface + shadow-lg + 16px 圆角，行高 44px；danger 变体走 destructive 软底 |
| 建议选项 | `.suggest-menu` / `.suggest-option` | Chat 提及列表已验证：浮动胶囊选项 chips，输入框上方 |
| 头像 | `.avatar` / `.avatar-placeholder`（`-sm/-md/-lg`） | 圆形 `object-fit: cover`；占位符 primary 底 + primary-fg 字；28/32/36/56px |
| 弹窗/Toast | `.modal-*`、`.toast-*` | Toast `z-80` 高于 Modal `z-70`；Toast 带进度条与进入/离开动画 |
| 表格 | `.table-shell` | 表头 surface-2 + muted 小字；行 hover surface-2/60 |
| 表格空状态 | `.table-empty-row` | 居中 muted 弱化文字；容器 `:has()` 虚线提示 |
| 复选框/单选/文件 | `input[type=checkbox|radio]` + `.field-check` + 文件按钮 | 18px 控件、`accent-color` 主色；文件按钮 surface-2 → hover primary-soft |
| 分页 | `.pagination` / `.pagination-info` | 弹性间距、信息区 muted；`aria-disabled` 禁用态 pointer-events none |
| 面包屑 | `.breadcrumb` / `.breadcrumb-sep` | muted 链接、border 分隔、`aria-current="page"` 加粗 |
| 页脚 | `.site-footer` / `.site-footer-inner` / `.filing-icon-placeholder` | Pass/Panel 已验证：`<footer class="site-footer"><div class="site-footer-inner">…</div></footer>`，`mt-auto` 贴底 + 半透明表面 + backdrop-blur；版权/备案/链接全部由 `brand.ts` 驱动（© 年份/版权方、ICP/公安备案、`FOOTER_LINKS`、GitHub、开源协议、反馈问题、联系我们）；Panel 变体以运行时 `site_settings` 为事实来源（`APP_VERSION` / `footer_text` / 备案图标缺失时 `.filing-icon-placeholder` 字形方块占位）；尺寸规格：单行高 56px（`text-xs` 12px/行高 16px + `py-5` 上下 20px，`min-h-14` 兜底）、图标/占位 14×14px、`gap-x-2`（8px）/`gap-y-1`（4px）、`max-w-7xl` 居中（`px-4` → `lg:px-8`），移动端换行、无横向滚动 |
| 进度条 | `.progress` / `.progress-bar`（`-sm`、`.is-success/.is-danger`） | 6–8px 胶囊轨道 + primary 填充，只动 width |
| 列表筛选行 | `.list-filters` | 搜索框 + 下拉 + 按钮等高（36px）成行；移动端搜索全宽、下拉自适应 |
| 紧凑按钮 | `.btn-sm` | 36px 紧凑密度；移动端仍用 `.btn` 保 44px 热区 |
| 标签栏 | `ScrollTabs`、`PillTabs` | 单行横滑、隐藏滚动条、snap 吸附、活动标签自动居中；PillTabs 依赖 gsap，按需引入 |
| 概览网格 | `MagicBento` | 深色 Bento 卡 + 光标聚光；依赖 gsap，按需引入；移动端与 reduced-motion 下自动静置 |
| 氛围层 | `FloatingBackground` + `useFloatingBackground` | 纯 Canvas 复合运动（水平漂移 + 垂直正弦），无第三方依赖；Chat `ambient.js` / Blog React 版落点见 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md) §3 |
| 极光层 | `AuroraBackground`（`.aurora` / `.aurora-blob`） | 4 枚弥散光斑（18/22/28/24s，`alternate`）；full=4 / soft=2；`.aurora-soft` 供工作台/后台降浓度；完整 CSS 已内置模板 |
| 科技光效层 | `TechAmbience`（`.tech-grid` / `.tech-beam` / `.tech-dot`） | 缓移网格 12s + 3 条错峰光束 10s + 8 枚光点 6s；认证默认、工作台/后台 `soft`；Blog 去光束变体（网格 + 8 枚强调色光点）；**核对关键帧已定义** |
| 主题切换 | `ThemeToggle`、`useTheme` | 存储键来自槽位 17；首帧前内联脚本应用 `html.dark` |
| 文字浮现 | `BlurText`（`motion/react`）；零依赖 `.blur-unit` | 按词/字错峰模糊浮现（450ms、35ms 错峰）；`prefers-reduced-motion` 静态渲染 |
| 数字滚动 | `CountUp`（`motion/react` 弹簧）；零依赖 `countUp` | 全部「共 N…」与统计数值；无 rAF/reduced-motion 直接落定目标值 |
| 滚动视差 | `HeroFX`（Blog 已验证） | 首屏滚动映射 scale 1→0.82 / y −30px / opacity 1→0.35 / blur 0→5px；阅读页禁用；reduced-motion 静态 |
| 本地徽章 | `badge` 本地 SVG 胶囊（Blog 已验证） | 公开站禁止 shields.io 外链：官方品牌色圆点/整块底 + 白字 + 本地图标；README 仍按 Li&About 规范用 shields.io |
| 反馈微件 | `PageSkeleton`、`shimmer`、`.spinner`、`.btn-ripple` | 入场 150–350ms；骨架扫光用 `background-position` |

**按钮状态纪律（V1.2）**：成对/并列按钮的 pending 状态**只属于被点击的按钮**——各按钮独立
action 或按目标区分状态，其它按钮仅 `disabled` 防并发；触发按钮与确认弹窗分离时，运行状态只显示在
弹窗确认按钮上；不要两个按钮同时转圈误导用户。

**移植纪律**：只移植需要的组件；带 gsap 的组件（PillTabs/MagicBento/StrokeText）确认体积与 CSP 约束后再引入；生产环境 `style-src 'self'`（无 `unsafe-inline`），动效必须尊重 `prefers-reduced-motion`。**禁止从任一项目仓库复制组件**——模板已含全部验证效果；确需项目特有模式时先回写模板（§7）再引用。

**零依赖原则（V1.3，Chat 已验证）**：若项目坚持「不加载远程资源 / 无第三方依赖」（如原生静态站），BlurText、CountUp、签名描边、流光线、涟漪、数字滚动、文字浮现全部有原生等价实现，见附录 F。

---

## 6. 验收清单（Pre-Delivery Checklist）

- [ ] 无 emoji 充当图标（统一 SVG）
- [ ] 图标来自一致图标集（Heroicons/Lucide/内置 SVG）
- [ ] 所有可点击元素有 `cursor-pointer`
- [ ] 下拉/菜单控件键盘完整（ArrowUp/Down/Home/End/Enter/Space/Escape）且 `aria-expanded` / `aria-selected` / `role=listbox|option` 同步
- [ ] 原生 select 与 `.input` 等高、焦点 ring 一致；复选框/单选 `accent-color` 主色；文件选择按钮 hover/focus 有过渡
- [ ] hover 状态有 150–300ms 平滑过渡
- [ ] 浅色模式正文对比度 ≥ 4.5:1
- [ ] 键盘焦点可见（`focus-visible` 2px 主色描边）
- [ ] `prefers-reduced-motion` 已尊重
- [ ] 响应式：375px / 768px / 1024px / 1440px 四档
- [ ] 无内容被固定导航遮挡
- [ ] 移动端无横向滚动
- [ ] 令牌无硬编码 hex（组件内），文案无硬编码（从 `brand.ts` 读取）
- [ ] 明暗模式切换无闪烁、无对比度丢失
- [ ] 全淡色口径（若采用）：无粉色系、无大面积重色；强调色 strong-on-soft ≥ 4.5:1
- [ ] 浅色语义色采用 V1.3 调校值（muted `#64736C` / success `#2A7C52` / warning `#9A5C05` / destructive `#C43737`），对底色对比 ≥ 4.5:1
- [ ] 深色下带文字的软底组件回退 `*-soft-solid` + `*-soft-fg`（实色粉彩底 + 深字 ≥ 8:1），不用 rgba 软底配同色浅字
- [ ] 每个 `animation` 都有对应 `@keyframes`（尤其科技光效层三组关键帧）
- [ ] 成对/并列按钮的 pending 只出现在被点击的按钮上
- [ ] 公开站（如博客）徽章为本地 SVG 胶囊，无 shields.io 外链；README 例外
- [ ] 新效果/新调校已先回写本模板（若本仓库为项目起点，本项自动满足）

**动效专项验收**：

- [ ] 所有飘动元素 `animation-iteration-count: infinite`
- [ ] 各页元素数量与 4.3 浓度分层一致
- [ ] `animation-delay` 已错峰，无两个元素同时从同侧进入
- [ ] 表单聚焦时循环速度减半、列表页滚动联动（0.5x–1.5x）
- [ ] 表格/核心阅读区无循环元素侵入
- [ ] 移动端（<768px）元素数 ≤ 6
- [ ] `prefers-reduced-motion` 下循环静止为单帧
- [ ] 滚动视差（HeroFX）只在非阅读页使用，reduced-motion 下静态渲染
- [ ] BlurText/CountUp 在 reduced-motion 或无 rAF 环境下直接落定最终内容
- [ ] Chrome Performance 录制 60s：无 Layout Shift，GPU 内存稳定

---

## 7. 治理与演进规则

- **变更流程**：新视觉决策先写 BRAND.md（意图 + 理由）→ 再在 `index.css` 以令牌落地 → 复用既有组件模式 → 对照本文档差距自查。
- **防跨项目复制（V1.3 硬规则）**：任何项目禁止从其他项目复制样式/组件文件；一律从本仓库实例化。发现新效果、新调校、新组件模式时**先回写本模板**（含参数、理由与验收证据），再在项目内引用；不允许「先落项目、后补模板」。实现总览见 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md) §5。
- **允许偏离的情形**：主色因产品域调整（走 3.1 取色方法）；符号隐喻重映射；确需新模式时先写 spec 再更新 MASTER.md 页面模式清单。**Li&Pass 2026-08-17 已按用户明确指令偏离**：全站切换海玻璃全淡色系（无粉无重）、新增科技光效层并接入后台、按钮改半透明着色——已在项目 `design-system/lipass/DESIGN-SOLUTION.md` 与 BRAND.md V2.x 记录理由。
- **禁止偏离的情形**：五大原则、动效铁律、单一事实来源分层、无障碍/节能底线。
- **漂移治理**：任何 PR 涉及视觉，对照第 6 章清单与项目 BRAND.md 差距表自查；代码与文档冲突时以代码为事实，并回写文档。
- **历史差异处理**：Li&Pass / Li&Panel 仍使用 V1.2 旧语义色（muted `#71807A` / success `#2F8F5F`），Li&Chat / Li&Blog 已用 V1.3 调校值。存量项目后续做无障碍审计时按调校值对齐；新项目一律从调校值起步。

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
| T1 填槽位 | 第 3 章槽位 1–22 | `design-system/<project>/BRAND.md` | 本方案 | 22 项齐全、每项有决策理由 |
| T2 令牌落地 | 第 4.1 节、槽位 7–12/16 | `frontend/src/index.css` | T1 | 无 `{{PROJECT_PREFIX}}` 残留、明暗两套齐全 |
| T3 品牌单点 | 槽位 1/3/18、3.2 资产规则 | `frontend/src/lib/brand.ts` | T1 | 品牌文案仅存在于该文件 |
| T4 浏览器品牌位 | 槽位 16/17/20 | `frontend/index.html` | T1、T3 | favicon / theme-color / description / 首帧主题脚本齐全 |
| T5 组件与页面外壳 | 第 5 章、4.3 节 | `frontend/src/components/`、`frontend/src/pages/` | T2 | 组件无硬编码 hex/文案，外壳符合 4.3 |
| T6 氛围层与主题 | 2.4 节、槽位 17/19 | `FloatingBackground` 接入 + `useTheme` | T2 | 浓度分层正确、reduced-motion 收敛单帧 |
| T7 验收 | 第 6 章 | `design-system/<project>/MASTER.md`、`preview/` 截图 | 全部 | 清单全勾 + 对比度数值 + 截图 |

**并行规则**：T2/T3/T4 依赖 T1，先 T1 后并行 T2–T4；T5/T6 依赖 T2，可并行；T7 最后串行。任意时刻每个文件只有一个 owner；需要改他人文件先认领并经 root 同意；并行数量不超过可用并发槽位。T5 与 T6 同处组件目录，须按组件类名细分所有权，确保不编辑同一文件。

> 前端结构与默认假设不同时（如 Li&Chat 当前为 `static/` 原生静态页），T2–T6 的文件路径按项目实际结构映射，令牌落地为项目实际样式文件；映射方式先在 T1 的 BRAND.md 中写明。

> **V1.3 补充**：T1 前先读 [PROJECTS-IMPLEMENTATION-INDEX.md](PROJECTS-IMPLEMENTATION-INDEX.md) 确认家族现状；T5 只从模板组件库移植，禁止从其他项目复制；新效果在 T7 验收通过后回写模板（§7 防跨项目复制）。

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
| 海玻璃全量方案（V1.2 决策时间线与完整令牌） | `参考实现 DESIGN-SOLUTION.md`（本次视觉刷新汇总） |
| AA 调校语义色（muted/success/warning/destructive）与 soft-solid/soft-fg 深色软底 | Li&Chat BRAND.md/MASTER.md + `static/style.css`；Li&Blog `tokens.css`（已采纳调校值） |
| 零依赖等价实现（blur-unit / countUp / ripple / card-signature / flow-line / ambient.js） | Li&Chat MASTER.md + `static/style.css` + `static/ambient.js` |
| HeroFX 滚动视差、本地徽章、打印/代码高亮令牌、data-ambient 氛围分级 | Li&Blog BRAND.md/MASTER.md + `web/src/*.jsx` + `tokens.css` |
| 1:1 复刻反例、面板网格 1→2→3→4、site_settings 品牌后台覆盖 | Li&Panel BRAND.md/MASTER.md |
| README 徽章与结构规范 | Li&About README.md → 已内联 [reusable-readme.template.md](reusable-readme.template.md) |

## 附录 B：令牌快照（供对照与回滚）

### B.1 Li&Pass 历史快照（V1.2 模板原值，Li&Pass / Li&Panel 仍在使用）

浅色模式（`:root`，海玻璃）：

| 角色 | 值 |
| --- | --- |
| bg / surface / surface-2 | `#F6FBF9` / `#FFFFFF` / `#EEF6F3` |
| fg / muted / border | `#35423F` / `#71807A` / `#E1ECE8` |
| primary / hover / soft / fg | `#25786D` / `#1F6359` / `#D9F4EE` / `#FFFFFF` |
| secondary / soft | `#2F678F` / `#DFF1FA` |
| success / warning / destructive | `#2F8F5F` / `#A16207` / `#CF3D3D` |
| ring | `#25786D` |
| 强调色 ice / aqua / lilac | `#2F678F` / `#25786D` / `#51488F`（soft `#DFF1FA`/`#D9F4EE`/`#EDEAFB`） |
| 强调色 sage / mint / sand | `#557546` / `#2F7C52` / `#876741`（soft `#EAF2E3`/`#E3F6E9`/`#F7EFE0`） |
| 按钮 / 文字 | bg `rgba(47,127,116,.10)`、hover `.17`、描边 `.26`；文字 `#24433E` |

深色模式（`.dark`，D1 雾灰）：

| 角色 | 值 |
| --- | --- |
| bg / surface / surface-2 | `#3A3F45` / `#434950` / `#4B5259` |
| fg / muted / border | `#F0F2F4` / `#B8C0C7` / `#545C64` |
| primary / hover / soft / fg | `#7FD4C6` / `#A5E4D9` / `rgba(127,212,198,.16)` / `#17332E` |
| secondary / soft | `#A8D4F0` / `rgba(168,212,240,.16)` |
| success / warning / destructive | `#86D6AC` / `#EAD48E` / `#E8A49A` |
| ring | `#7FD4C6` |
| 强调色 ice / aqua / lilac | `#A8CBE8` / `#7FD4C6` / `#B0A8DE`（soft 同色 16–18% rgba） |
| 强调色 sage / mint / sand | `#B0C79E` / `#9ADFAD` / `#D9C49E` |
| 按钮 / 文字 | bg `rgba(127,212,198,.13)`、hover `.21`、描边 `.30`；文字 `#D7EFEA` |

### B.2 V1.3 家族调校值（推荐默认，Chat / Blog 已验证）

浅色模式仅四处与 B.1 不同（同色相加深，AA 达标）：

| 角色 | V1.2 旧值 | V1.3 调校值 | 对底色对比度 |
| --- | --- | --- | --- |
| muted | `#71807A` | `#64736C` | 3.96 → 4.77 |
| success | `#2F8F5F` | `#2A7C52` | 3.85 → 4.89 |
| warning | `#A16207` | `#9A5C05` | 4.71 → 5.14 |
| destructive | `#CF3D3D` | `#C43737` | 4.58 → 5.09 |

深色模式新增深色软底实色粉彩令牌（带文字组件回退目标，对比 8.0–8.9）：

| 角色 | soft-solid | soft-fg |
| --- | --- | --- |
| primary | `#D9F4EE` | `#17332E` |
| success | `#E3F6E9` | `#14532D` |
| warning | `#FDF3D8` | `#78350F` |
| destructive | `#FDEEEE` | `#7F1D1D` |

按钮扫光令牌：浅色 `--*-btn-sweep: rgba(255,255,255,.42)`；深色 `rgba(255,255,255,.18)`。
极光令牌：浅色 `--*-aurora-1..4` = `rgba(127,212,198,.32)` / `rgba(143,199,240,.30)` / `rgba(169,162,232,.26)` / `rgba(169,204,143,.24)`；深色 = `.40` / `.36` / `.32` / `.28`（同色相）。

阴影与动效：`--shadow-sm/md/lg` 三档水绿 tint 弥散阴影（透明度总和 < 0.1）；`--ease-out`（入场）、
`--ease-spring`（按压/弹窗）；`--motion-fast/base/slow = 150/250/350ms`。科技光效层节奏：
网格 12s、光束 10s（错峰 0.8/4.2/7.5s）、光点 6s；极光四斑 18/22/28/24s；签名描边 9s、
流光线 5s、按钮扫光 4s、卡片辉光 4.5s；文字浮现 450ms（35ms 错峰）；涟漪 500ms。

## 附录 C：规则库交叉验证结论

本方案的通用标准与 ui-ux-pro-max 规则库交叉验证（2026-08-16 检索）：

- **color / `trust security corporate blue`**：首位结果（Insurance Platform）主色 `#0369A1`、Ring `#0369A1`、Destructive `#DC2626`，与 Li&Pass 主色一致；Notes 明确「Security blue + protected green [Accent adjusted for WCAG 3:1]」。
- **typography / `corporate trust professional`**：首位「Corporate Trust」组合 Lexend（标题）+ Source Sans 3（正文），Notes「Lexend designed for readability. Excellent accessibility.」——与参考实现 BRAND.md §3.2 的自托管建议一致，正文保持系统字体栈 + 中文回退。
- **ux / `reduced motion accessibility performance`**：三条均 Severity High——必须检查 `prefers-reduced-motion`、避免强制滚动特效、每个视图最多动画 1–2 个关键元素。与本方案 2.4 铁律一致。
- Li&Pass 设计时已验证：`--design-system "sso identity authentication security trust enterprise portal"` 输出「Enterprise Gateway / Trust & Authority」模式，主色同为 `#0369A1`（见参考实现 BRAND.md 附录）。
- **V1.2 更新（2026-08-17）**：海玻璃主色由 `aurora-ui` / Web3 紫科技等检索结果淡色化推导，经 WCAG AA 核算后按用户指令定稿为 `#2F7F74`；**V1.3（2026-08-20）按各项目代码事实统一为 `#25786D`**（`#2F7F74` 仅存于模板早期文档，落地代码从未使用）。早期「Trust & Authority」安全蓝结论仅作历史记录。

## 附录 D：实例化样例与后续建议

- **首个实例化样例**：Li&Pass。本方案按其提炼；其项目内已具备 `design-system/<project>/BRAND.md` 与 `MASTER.md`，符合 §1.2 的要求。
- **视觉对齐参照**：各项目把页面截图/预览保存在各自 `design-system/<project>/preview/`，作为项目内对照基准；本仓库不提供外部图片引用。

## 附录 E：RGB 色值调校方法（速查，完整版见 Li&Pass DESIGN-SOLUTION.md §11）

所有色值改在落地令牌的 `:root`（浅）与 `.dark`（深）两处；只调「H 色相、S 饱和、L 亮度」三个量：

1. **基础直觉**：三通道同加/同减 = 调亮度（色相基本不变）；通道差距 = 饱和度；差距小 = 雾面。改亮度优先在 HSL 空间固定 H/S、只动 L。
2. **角色目标档**（海玻璃基准）：浅 bg `L≈96–98%`、浅 fg `L≈18–25%`、浅主色/强调色取 600–700 档（`L≈33%`）；深 bg 雾灰 `L≈22–28%` 不压黑、深 fg `L≈88–95%`、深主色/强调色取 300 档（`L≥70%`）；soft 底色 = `rgba(strong, 0.14–0.18)`；按钮 = `rgba(主色, 0.10–0.13)` + 描边 ×2.5–3。雾面感 = `S ≤ 25%`（>35% 即「艳」）。**V1.3 起浅色语义色已内置调校值（附录 B.2），新项目直接采用，无需再调。**
3. **对比度核算**：`lin(c) = c/255 ≤ 0.03928 ? c/255/12.92 : ((c/255+0.055)/1.055)^2.4`；
   `L = 0.2126·lin(R)+0.7152·lin(G)+0.0722·lin(B)`；`CR = (L亮+0.05)/(L暗+0.05)`；
   正文 ≥ 4.5、图形/大字 ≥ 3。fg/bg 与 strong/soft 两组必验。
4. **禁忌判据**：粉色/玫瑰系 = `R > G+30 且 B ≥ G-20`；大面积重色 = `L < 10%`（RGB 均值 < 26，Bento 小卡除外）。
5. **浅↔深映射**：保持 H/S，L 换互补档——bg 96–98%↔22–28%、fg 18–25%↔88–95%、主色 33%↔70%+。例：`#25786D`(H172°/S53%/L31%) ↔ `#7FD4C6`(H170°/S50%/L66%)。
6. **工作流**：定 H → 定 L（按角色表）→ 定 S（10–25%）→ 验对比（≥4.5）→ 扫禁忌（无粉无重）→ `:root`/`.dark` 成对落地并回写文档。

**深色软底上限（必读）**：`rgba(浅色, 0.14–0.18)` 软底上的同色浅字对比上限 ≈ 3.9，**不可能**达到
4.5。深色下需要文字时二选一：① 实色粉彩底 + 深色文字（`#17332E`，对比 7+）；② 文字改高亮近白浅色
（如 `#CFF0DE`）。只有图标/图形可以留在 3:1 档——徽章与瓦片文字务必按 ① 处理。

## 附录 F：零依赖等价实现清单（Chat 已验证）

模板默认组件的 motion/react / gsap 版本均可在「不加载远程资源」约束下用原生 CSS/JS 等价实现：

| 效果 | 零依赖实现 | 关键参数 |
| --- | --- | --- |
| 文字浮现 | JS 按词拆 `span.blur-unit`，设 `--blur-index`；CSS 450ms 错峰入场 | blur 8px、y 6px、35ms/词；reduced-motion 直达终态 |
| 数字滚动 | `countUp`：三次缓动（ease-out 分段） | 450ms；仅统计数值/计数徽章触发；无 rAF 直接落定 |
| 按钮涟漪 | 点击时注入 `span.btn-ripple`（大小 = 点击位置到四角最远距离），`animationend` 移除 | 500ms、currentColor、opacity 0.18→0 |
| 签名描边 | `.card-signature::after` mask 环（`mask-composite: exclude`） | 9s、`background-position` 0→200% |
| 流光线 | `.flow-line`（顶栏底部绝对定位） | 5s、200% 背景位、opacity 0.7 |
| 极光层 | `.aurora` / `.aurora-blob` ×4（radial-gradient，无 filter 动画） | 18/22/28/24s alternate |
| 科技光效层 | `.tech-grid` / `.tech-beam` / `.tech-dot` 纯 CSS | 12s / 10s 错峰 / 6s；关键帧齐全 |
| Canvas 氛围层 | `ambient.js`：rAF 绘制 line/square/z/dot，读 CSS 令牌颜色 | 浓度可调（`setDensity(n)`）；DPR≤2；移动端 ≤6；reduced-motion 单帧 |
| 自定义下拉 | JS 渐进增强：隐藏原生 select + `button[aria-haspopup=listbox]` + `ul[role=listbox]` + `li[role=option]`，保持原生 select 为表单事实源 | ArrowUp/Down/Home/End/Enter/Space 开合选择、Escape 关闭、外点关闭、选择后派发 `change`（bubbles）；`aria-expanded` / `aria-selected` 同步 |

选择原则：有构建链与体积预算 → 用模板默认（motion/react）；原生静态站 / 零外部资源 → 用本附录。
