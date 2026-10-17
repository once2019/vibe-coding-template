# AGENTS.md — vibe-template 仓库协作规范

> 本文件是 vibe-template 仓库自身的协作规范（吃自己狗粮的精简版），不是模板——模板唯一正本在 `skills/vibe-init/assets/`，接入新项目时经 vibe-init 技能安装，勿手工复制本文件。

## 概述

- 定位：vibe coding 治理模板的 skill 正本仓库；产出 vibe-init / vibe-memory / vibe-governance 三个治理技能，不是业务项目。
- 结构：`skills/vibe-init/`（SKILL.md + assets/ 模板唯一正本 + scripts/ 脚手架）；本仓库自身的决策记录在 `docs/decisions/`。

## 纪律

- 模板唯一正本 = `skills/vibe-init/assets/`；任何位置不得维护第二份模板副本。
- 修改 assets 下的模板规则前，先在 `docs/decisions/` 登记决策记录（格式沿用 `skills/vibe-init/assets/docs/decisions/_template.md`）；占位符文字微调不需决策。
- SKILL.md 的触发词与工作流程变更同样视为治理决策，须登记。
- 脚手架脚本只用 Python 标准库，不引入第三方依赖。
- 本文件 ≤40 行；治理细则的完整形态见模板本体，不在此复述（唯一事实来源原则）。

## 命令

- 验证脚手架：`python3 skills/vibe-init/scripts/init_vibe_project.py <临时目录>` 连跑两遍，第一遍全新建、第二遍全跳过，且占位符清单只含应填文件。
- 技能校验打包：`python3 <skill-creator>/scripts/package_skill.py skills/vibe-init <输出目录>`，校验不通过不得交付。
- 规则：提交前上述检查必须通过，展示命令输出作为证据。
