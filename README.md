# Li&Design · 可复用设计模板

Li& 系列产品的共用品牌/视觉设计模板仓库：从 Li&Pass 已验证的设计系统提炼，供所有子项目（Li&Chat 及后续新项目）按「填槽位 → 复制令牌 → 过验收」的方式实例化。

## 目录结构

| 文件 | 用途 |
| --- | --- |
| [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) | 主方案：品牌内核（不变层）+ 项目适配槽位表（20 项）+ 落地流程 + 组件库 + 验收清单 |
| [reusable-tokens.template.css](reusable-tokens.template.css) | Tailwind CSS 4 令牌骨架，含 `{{PROJECT_PREFIX}}` 占位符与明暗两套色板 |

## 快速上手（新项目 3 步）

1. 复制 `reusable-tokens.template.css` 到新项目 `frontend/src/index.css`，把 `{{PROJECT_PREFIX}}` 换成项目技术标识（如 `lipass`、`chat`），按槽位表填色值。
2. 按 [REUSABLE-BRAND-SCHEME.md](REUSABLE-BRAND-SCHEME.md) 第 3 章逐项填写适配槽位（名称、定位、主色、语义色、字体、Logo、氛围浓度等）。
3. 按第 4 章搭建组件与页面外壳，最后过第 6 章 Pre-Delivery Checklist。

## 核心原则（速记）

- 信任优先、克制科技感、以动衬静、单一事实来源、无障碍节能。
- 60/30/10 用色比例；深色 = 去饱和浅色调变体；主色永远小面积强调。
- 动效只动 `transform/opacity`，尊重 `prefers-reduced-motion`，移动端减量省电。
- 令牌只存在 `index.css`，品牌文案只存在 `brand.ts`，组件禁止硬编码。

## 参考实现

文档正文中指向 `../Li&Pass/...` 的路径为本机相邻的参考实现（提取来源与对照样例）。本仓库内容自包含，克隆到其他位置时这些路径仅作信息性引用。

## 治理

- 新视觉决策先写 BRAND.md 意图，再以令牌落地；代码事实与文档冲突时以代码为准并回写文档。
- 首次实例化样例：`../Li&Pass`；首个适配候选：`../Li&Chat`（差距与步骤见 REUSABLE-BRAND-SCHEME.md 附录 D）。
