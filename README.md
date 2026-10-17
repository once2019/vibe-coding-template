# vibe-template

vibe coding 治理模板的 **skill 正本仓库**。模板本体（`AGENTS.md` + `docs/`）存放于 `skills/vibe-init/assets/`，通过 `vibe-init` 技能安装到目标项目；本仓库不再维护第二份模板副本。

## 解决什么问题

### 会话一长，Agent 就失忆

上下文满了，开个新会话，Agent 把上周定的方案忘得一干二净。你重新解释一遍，它重新问一遍，一周下来你怀疑自己是在编程还是在给 AI 补历史课。

模板用三层记忆对抗上下文丢失：

- L1 = `AGENTS.md`，常驻，只放红线和目录
- L2 = `docs/decisions/`，每个技术决策一条记录，含理由和被否决的方案
- L3 = `docs/memory/`，当前状态快照（context.md）和跨会话交接（handoff.md）

新会话先读 L3，再查决策索引最近三条（相关才展开全文）再动手。上下文不用"记住"所有事，只需要知道去哪查。

### 决策的理由埋在聊天记录里

"当时为什么用轮询不用 WebSocket？"答案在三天前的对话记录里，没人翻得动。下个会话的 Agent 看了眼代码，觉得 WebSocket 更优雅，推翻了它，没人意识到这是重复踩坑。

`docs/decisions/` 强制每个影响方向的决策留痕：决定了什么、为什么、否决了什么、影响哪里。每条决策同步登记进 `docs/decisions/README.md` 索引，一行一条，新会话起步只读索引摘要。小补充走文末带日期的追记节，方向性推翻另建新条说明理由，修订历史不覆盖。

### 规则写了好几遍，互相矛盾

`.cursorrules`、`CLAUDE.md`、copilot 的说明文件，再加上一段贴在 prompt 里的——四处规则，改一处漏三处，Agent 读到哪份算哪份。

`AGENTS.md` 是唯一事实来源。规则只收 Agent 读代码发现不了的信息，每行先过一遍：删掉它，Agent 会犯错吗？不会，就删。重复配置不允许存在第二份。

### Agent 说"完成了"，其实没跑

"已修复。"测试没跑，lint 没过，类型检查一片红。你信了，合并了，CI 教你做人。

规范写明：提交前检查必须全部通过，禁止跳过验证直接宣称完成，必须贴命令输出当证据。测试全绿只证明能跑，不证明对。

### 代码改了，文档没动

接口签名变了，`docs/design/` 里还是三个月前的图。下个会话的 Agent 照旧文档写新代码，错得理直气壮。

同步规则写进了流程：需求变更先改 `docs/specs/` 再动代码；设计变了必须更新 `docs/design/` 并标注变更原因；代码和文档不一致，任务不算完成。

### AI 生成的代码没人评审就进主干

Agent 十分钟写了五百行，看着挺像回事。没有人类评审，合并，上线，出事。

红线钉死：AI 生成的代码未经人类评审不得合并或部署；认证、加密、输入校验一律用成熟库，禁止自研安全原语；危险操作（删数据、force push、改 CI、引入新依赖）执行前必须经人类确认，全部集中在 `AGENTS.md` §4 的 Ask-first 集中清单里，新增事项登记一处，别处只作出处引用。

### 上下文被历史堆满

把所有过往对话堆在会话里，token 烧得飞快，关键信息还被淹没。

记忆按需分层加载：状态快照只记当前，完成项移交 `docs/progress/` 后即删，决策索引只留最近三条文件名，全文有行数与单行长度双上限。快照是状态，不是日志。

## 安装技能

把三个技能目录复制到 CodeBuddy 的用户技能目录：

```bash
mkdir -p ~/.codebuddy/skills && cp -r skills/vibe-init skills/vibe-memory skills/vibe-governance ~/.codebuddy/skills/
```

安装后：对新项目说「初始化项目治理 / init AGENTS」触发 vibe-init（脚手架生成骨架，不追问占位符）；写记忆与决策时 vibe-memory 按细则介入；治理信号出现时 vibe-governance 接管规则维护与复盘。

## 仓库结构

```text
├── AGENTS.md               # 本仓库自身的协作规范（非模板）
├── README.md               # 本文件
├── docs/decisions/         # 本仓库自身的决策记录
└── skills/
    ├── vibe-init/          # 治理骨架初始化：SKILL.md + assets 模板唯一正本 + scripts 脚手架
    ├── vibe-memory/        # L2/L3 写作细则：context/handoff/决策记录怎么写才合格
    └── vibe-governance/    # L1 维护与治理复盘：规则怎么改、复盘怎么跑
```

## 修改纪律

- 改模板 = 改 `skills/vibe-init/assets/` 下的文件；模板规则变更须先在 `docs/decisions/` 登记决策记录。
- 提交前验证：脚手架在临时目录两遍运行（新建 + 幂等）通过，且官方 `package_skill.py` 校验通过；展示命令输出。
- 规范细节见本仓库 `AGENTS.md`。

## 这个模板长这样，是复盘出来的

模板在真实项目实战一周（54 条决策）后做了一轮治理复盘：8 个反模式（入口膨胀、压行不压量、规则相抵、决策无索引、Ask-first 散落、易腐运行态、bootstrap 膨胀、不可测触发）各有实测证据与改法，已全部固化进模板本体。证据与自查清单见 `skills/vibe-init/assets/docs/design/governance-retrospective.md`。

## 这个模板不做什么

不规定技术栈，不替你写代码，不保证 Agent 不出错。它只解决"人和 Agent 如何跨会话协作"这一层：记忆不丢、决策可查、规则唯一、验证留证。代码质量由你的评审把关，这是红线里唯一不能被自动化替代的部分。
