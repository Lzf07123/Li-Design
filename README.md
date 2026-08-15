# Li&Design · 可复用设计模板

> ⚠️ **使用边界：本仓库仅在项目第一次设计时参考。** 每个项目必须在自己的仓库中生成适用于当前项目的设计方案（`design-system/<project>/BRAND.md` + `MASTER.md` 与落地令牌）。首次设计完成后，后续开发一律以项目内方案为准，不再依赖本仓库。

Li& 系列产品的共用品牌/视觉设计模板仓库：从 Li&Pass 已验证的设计系统提炼，供所有子项目（Li&Chat 及后续新项目）按「填槽位 → 复制令牌 → 过验收」的方式实例化。

## 目录结构

| 文件 | 用途 |
| --- | --- |
| [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) | 主方案：品牌内核（不变层）+ 项目适配槽位表（20 项）+ 落地流程 + 组件库 + 验收清单 + 多 Agents 协作方法（第 8 章） |
| [reusable-tokens.template.css](reusable-tokens.template.css) | Tailwind CSS 4 令牌骨架，含 `{{PROJECT_PREFIX}}` 占位符与明暗两套色板 |
| [AGENTS.md](AGENTS.md) | 模板仓库的多 Agents 协作手册：事实来源、硬性规则、协作规范、验证命令 |

## 快速上手（新项目 3 步）

1. 复制 `reusable-tokens.template.css` 到新项目 `frontend/src/index.css`，把 `{{PROJECT_PREFIX}}` 换成项目技术标识（如 `lipass`、`chat`），按槽位表填色值。
2. 按 [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) 第 3 章逐项填写适配槽位（名称、定位、主色、语义色、字体、Logo、氛围浓度等）。
3. 按第 4 章搭建组件与页面外壳，最后过第 6 章 Pre-Delivery Checklist；多 Agents 协作实例化见第 8 章。

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
- 60/30/10 用色比例；深色 = 去饱和浅色调变体；主色永远小面积强调。
- 动效只动 `transform/opacity`，尊重 `prefers-reduced-motion`，移动端减量省电。
- 令牌只存在 `index.css`，品牌文案只存在 `brand.ts`，组件禁止硬编码。
- 多 Agents 协作：单一事实来源、一个任务一个 owner、并行任务零文件重叠（方案第 8 章 + [AGENTS.md](AGENTS.md)）。

## 参考实现

本仓库内容自包含，不依赖任何相邻目录或外部链接；文中引用的 Li&Pass 令牌与槽位示例已内联在文档中，克隆到任意位置均可直接使用。

## 治理

- 新视觉决策先写 BRAND.md 意图，再以令牌落地；代码事实与文档冲突时以代码为准并回写文档。
- 示例取值来自首个实例化项目 Li&Pass（已内联于方案文档附录 B）；新项目按第 3 章填自己的槽位，不引用外部仓库。
- 本仓库只承载模板的演进；各项目的设计方案在各自仓库内独立演进。
- 多 Agents 协作遵循 [AGENTS.md](AGENTS.md) 与方案第 8 章：并行任务零文件重叠，root agent 只按验证输出验收。
