# Li&Design 项目协作手册（多 Agents）

> 本文件是给后续 AI Agent（Codex 等）的「项目宪法」。**新会话必须先完整读完本文件再动手；子 agent 接单后同样先读本文件与第二节事实来源。** 人类开发者同样适用。

## 一、项目是什么

Li&Design 是 Li& 系列产品的共用品牌/视觉设计模板仓库：从 Li&Pass 已验证的设计系统提炼，供 Li&Chat 及后续新项目按「填槽位 → 复制令牌 → 过验收」实例化。

**使用边界（最重要）**：本仓库只在项目**第一次设计**时参考。首次设计完成后，各项目必须生成自己的 `design-system/<project>/BRAND.md` + `MASTER.md` 与落地令牌，此后以项目内方案为准；本仓库不作为任何项目的运行时依赖。

## 二、事实来源（动手前按顺序读）

| 内容 | 位置 |
| --- | --- |
| 概览、目录结构、快速上手、治理 | [README.md](./README.md) |
| 主方案：品牌内核 + 22 项槽位表 + 落地流程 + 组件库 + 验收清单 + 多 Agents 协作方法（§8） | [REUSABLE-BRAND-SCHEME.md](./REUSABLE-BRAND-SCHEME.md) |
| 令牌骨架（Tailwind CSS 4）：`{{PROJECT_PREFIX}}` 占位符与明暗两套色板 | [reusable-tokens.template.css](./reusable-tokens.template.css) |
| 可复用 README 模板：结构约定 + 徽章规则 + 写作原则 | [reusable-readme.template.md](./reusable-readme.template.md) |

**文档与代码冲突时**：`reusable-tokens.template.css` 是令牌事实，`REUSABLE-BRAND-SCHEME.md` 是意图。先核对差异，再决定改哪边；改一边必须同步另一边（见第六节）。

## 三、目录结构与分层

```text
README.md                        概览、快速上手、交付清单、治理
REUSABLE-BRAND-SCHEME.md         主方案（不变层 + 槽位层 + 执行层 + 协作方法）
reusable-tokens.template.css     令牌骨架（唯一代码事实）
reusable-readme.template.md      README 模板（结构/徽章/占位符）
AGENTS.md                        本手册
```

三层结构见方案 §1：品牌内核（不变）、项目适配槽位（逐项目重填）、落地模板（复制执行）。任何改动必须分清落在哪一层。

## 四、硬性规则

1. **保持使用边界**：任何改动不得让子项目产生对本仓库的运行时依赖；只做「首次设计参考」的模板演进。
2. **自包含**：不引用相邻目录或外部仓库路径；示例取值内联在文档中，克隆到任意位置即可用。
3. **单一事实来源**：颜色/阴影/动效只在 `reusable-tokens.template.css`；槽位表与验收清单只在 `REUSABLE-BRAND-SCHEME.md`；两边必须同步。
4. **分层不可混**：改品牌内核需明确理由并在方案中记录；示例取值来自 Li&Pass，新项目按第 3 章填自己的槽位。
5. **完成 = 验证 + 文档**：声称完成前给出第七节验证输出；涉及方案结构变更时同步 README。
6. **命名**：模板仓库为 `Li&Design`；`{{PROJECT_PREFIX}}` 只是占位符，子项目技术标识由其槽位 2 决定（如 `lipass`、`chat`），不在模板中固化任何项目前缀。

## 五、多 Agents 协作规范

**总原则：单一事实来源、一个任务一个 owner、并行任务零文件重叠。**

角色划分：

- **root agent**：拆解任务、指派、收集验证证据、验收，并对用户交付最终结果。
- **sub-agent**：执行一个明确的 Task，交付验证证据，不越权扩张。

派活规则：

1. 只派具体、有边界的 Task；附完整上下文，确保子 agent 无需猜测项目事实。
2. Task 必须写清 Consumes（依赖/输入文件）与 Produces（产出文件/契约），**精确到文件**，验收标准可独立验证。
3. 并行派发的 Task 之间不得重叠同一文件或同一契约；有依赖关系一律串行。
4. 并行数量不超过可用并发槽位；共享工作区改动即时可见，先认领再动手。

执行纪律（每个 agent 都适用）：

- 动手前先读本文件与第二节事实来源；不清楚就问 root，**不许用猜测代替调查**。
- 不擅自扩大任务范围；需要新决策时回报 root 或停下询问用户。
- 验证才算完成：跑第七节命令并保留输出；失败必须说明原因与证据。
- 遇阻先探原因（读文件、跑最小检查、对比历史提交），带着证据汇报，不静默停摆。
- 不做破坏性操作（`rm -rf`、force push、动他人提交）；不动他人未提交的改动；子 agent 不自行切换分支或合并 main。

评审与验收：

- 每个 Task 完成后做**两段评审**：① 是否符合方案内核/槽位/清单规范；② 质量门禁（占位符一致、链接有效、无自相矛盾）是否全绿。
- root 只依据**验证输出**验收，不接受无证据的「完成」声称。

冲突处理：

- 文档与代码冲突 → 以 `reusable-tokens.template.css` 为令牌事实，回写方案文档。
- agent 之间意见冲突 → 提交 root，用可复现的事实裁决。
- 与用户意图冲突或需要新权限/外部协调 → 停下当前动作，向用户说明并请求指示。

## 六、标准工作流

1. **调查**：按第二节读事实来源；`git log --oneline -10` 与工作区状态确认无人正在改同一文件。
2. **设计**：先在 `REUSABLE-BRAND-SCHEME.md` 写意图与理由（改内核须说明偏离理由，见方案 §7）。
3. **落地**：同步改 `reusable-tokens.template.css` 与 README 中受影响的部分；槽位表新增/改名必须同步检查令牌变量。
4. **验证**：跑第七节命令。
5. **收尾**：按第八节提交，保留 merge 记录。

## 七、验证命令

```bash
# 令牌模板占位符数量应恰为 128 处（V1.2 海玻璃：新增 secondary/六强调色/按钮着色/品牌文字/流光线/科技光效令牌）；新增/删除槽位令牌会改变此数
rg -F -o '{{PROJECT_PREFIX}}' reusable-tokens.template.css | wc -l

# 方案文档与令牌模板的引用一致性（如 --<prefix>-primary 应在 @theme/:root/.dark 中成对出现）
rg -n 'PROJECT_PREFIX|primary|surface-2' REUSABLE-BRAND-SCHEME.md reusable-tokens.template.css

# README 与方案文档的内部链接必须可解析（同目录文件存在）
ls README.md REUSABLE-BRAND-SCHEME.md reusable-tokens.template.css reusable-readme.template.md AGENTS.md
```

> 附录 B（Li&Pass 令牌快照）是回滚对照表：改模板色值时同步核对快照，避免明暗两套错位。

## 八、提交与分支

- 分支：`codex/<topic>`（kebab-case），完成后合并回 `main`（保留 merge 记录）。
- 提交消息：`<type>: <中文简述>`；type 用 `docs`（方案/手册改动）、`style`（令牌模板改动）、`feat`/`chore` 等。
- 每个 Task 独立提交，便于评审与回滚。

## 九、常见坑

- **子模块不会自动更新**：Li&Chat / Li&Pass 以子模块方式引用本仓库，模板改动后需在各自项目手动 `git submodule update --init`（对齐锁定提交），`--remote` 要评审后谨慎使用。
- **槽位表与令牌模板失配**：新增槽位（如新语义色）必须在模板中同步加变量，否则实例化时会漏令牌。
- **附录 B 与模板色值漂移**：两处都写有 Li&Pass 色值，改一处必须核对另一处。
- **占位符计数**：`{{PROJECT_PREFIX}}` 全文件 128 处是 V1.2 基准；只改一处容易造成明暗两套不一致。
- **科技光效层关键帧缺失**：只写 `animation` 引用、漏定义 `@keyframes` 会让网格/光束/光点完全静止（光束基态 `opacity:0` 且不可见）；实例化时逐一核对「每个 animation 都有 @keyframes」。
