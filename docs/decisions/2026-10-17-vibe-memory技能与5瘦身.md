# vibe-memory 技能与模板 §5 瘦身

- 日期：2026-10-17
- 状态：已生效
- 相关模块：`skills/vibe-memory/`（SKILL.md + references/memory-writing.md + references/decision-writing.md）、`skills/vibe-init/assets/AGENTS.md` §5

## 决策内容

新增 vibe-memory 技能承载 L2/L3 写作细则（SKILL.md 触发路由 + 两份 references：memory-writing、decision-writing）；模板 AGENTS.md §5 由 19 行瘦身为 8 条红线，只留红线、双预算与细则指针，细则移出常驻上下文按需加载。

## 选择理由

- 质量痛点（实测）：快照写流水账、handoff 塞易腐运行态、追记失范——`_template.md` 与各文件头部给了"长什么样"，没给"怎么写对"；判断性细则（何时建条、追记 vs 另建、快照收敛纪律）此前无处安放。
- 上下文痛点：§5 操作细节属"Agent 可按需获知"，常驻违反模板自身收录铁律，也是 ashare-lake 复盘反模式 #7（bootstrap 膨胀）的组成部分。
- 分工定型：红线常驻 AGENTS.md（加载可靠），细则按需 skill（语义触发）；未安装技能时模板仍自足（§5 指针回落到各文件头部说明与 _template.md），残余风险有兜底。

## 被否决的替代方案

| 方案 | 否决原因 |
| --- | --- |
| 细则全部留在 §5 不动 | 常驻成本持续累积；违反"只写 Agent 不可自行发现的信息"收录铁律 |
| 细则并入各文件头部说明 | 头部说明随之膨胀，是反模式 #2（行数预算被稀释）的变体；细则需要一处权威载体 |
| 连预算校验脚本一起实现 | 用户裁决后置：先实测细则价值，脚本等真实需求再上 |
| L1 维护与治理复盘一并装入 | 两类触发节奏与受众不同，混装使 description 失焦；留给未来 vibe-governance |

## 影响范围

- 涉及文件：`skills/vibe-memory/`（新增 3 文件）；`skills/vibe-init/assets/AGENTS.md` §5（瘦身）；`docs/decisions/README.md`（索引追加本条）。
- 兼容性：旧项目按旧 §5 运行不受影响；新接入项目直接用瘦身版；§5 语义等价（红线全保留）。
- 后续约束：L3/L2 写作细则的新增或修订 → 改 `skills/vibe-memory/references/` 并按需追记本决策；本技能不触碰 vibe-init 与 L1 治理。
