# vibe-governance 技能

- 日期：2026-10-17
- 状态：已生效
- 相关模块：`skills/vibe-governance/`（SKILL.md + references/l1-maintenance.md + references/governance-review.md）、`skills/vibe-init/assets/AGENTS.md` §8

## 决策内容

新增 vibe-governance 技能承载 L1 维护细则（收录铁律判定、写入查重、修订流程、优先级裁决、修剪）与治理复盘五步流程；模板 AGENTS.md §8 追加指针行。治理技能三件套（init / memory / governance）就此成型，覆盖项目生命周期：冷启动 → 日常写作 → 自我演化。

## 选择理由

- 素材正本已存在：`governance-retrospective.md` 的方法论（复盘五步、裁决原则、8 问、5 信号）经实战一周验证，但"怎么执行"此前无操作细则载体。
- 清单不复制：5 信号与 8 问的正本留在项目内 governance-retrospective.md，skill 只写流程与裁决规范并在 SKILL.md 标注正本位置——避免清单双正本分叉（反模式 #4 同源问题）。
- 分工清晰：L1 维护（低频、全局）与 L2/L3 写作（高频、局部）触发节奏与受众不同，独立 skill 使 description 各自聚焦。

## 被否决的替代方案

| 方案 | 否决原因 |
| --- | --- |
| 8 问/5 信号复制进 references | 清单两处分叉，违反唯一事实来源；正本修订时必漏一处 |
| 复盘细则并入 vibe-memory | 前一决策已裁决：两类触发节奏混装使 description 失焦 |
| 继续预留不做 | 用户裁决提前实施：素材成熟（实战一周的方法论正本），无需再等实测证据 |

## 影响范围

- 涉及文件：`skills/vibe-governance/`（新增 3 文件）；`skills/vibe-init/assets/AGENTS.md` §8（追加指针）；根 `README.md`（三技能安装与结构）、根 `AGENTS.md`（定位行）。
- 兼容性：未安装该技能的项目经 §8 指针回落到 governance-retrospective.md 方法论，模板仍自足。
- 后续约束：复盘信号定义变更须同步三处（governance-retrospective.md、SKILL.md 触发词、复盘文档末节）；L1 规则修订一律先决策后改文件。
