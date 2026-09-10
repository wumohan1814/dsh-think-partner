# idea-forge — DSH 想法锻造（思考搭档）

一个给 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)（DSH）使用的 **agent preset**。

不写代码，只靠深度推理，帮用户把一个**模糊的想法**经过「细化 → 落实 → 推进」的循环，变成清晰、可执行、可持续推进的成果。

---

## 它是什么

DSH 里每一项能力都是 `cordis.yml` 中的一行插件，而**一个 agent preset 决定一个会话贡献哪些工具与提示词段落**。`idea-forge` 就是这样一个 preset：

- **不编程** — 移除了 Shell、workflow、ralph 等面向编码与多代理编排的插件行
- **推理优先** — persona 内置结构化推理姿态、访谈协议与发散／收敛纪律
- **推进导向** — 文件读写（沉淀文档）、联网查证、goal 目标（跨会话推进）、子代理（委派事实查证）

## 安装

```powershell
# 1. 克隆
git clone https://github.com/wumohan1814/dsh-think-partner.git dsh-idea-forge

# 2. 把 idea-forge 目录复制进 DSH 的用户预设根目录
Copy-Item -Recurse dsh-idea-forge\idea-forge "$env:USERPROFILE\.dsh\.agent-presets\"
```

预设根目录是 `${DSH_HOME:-$HOME/.dsh}/.agent-presets/`，若你设置过 `DSH_HOME` 请相应替换。目录名就是预设 id，所以目标目录必须叫 `idea-forge`。

安装后重启 DSH，在预设选择器中选择 **「想法锻造（思考搭档）」**。

## 用法

不需要任何命令、配置或代码，直接把想法说给它听。

### 细化：访谈不是「一次问一句」，也不是「一次全问」

它把想法建成一棵**决策树**，每轮只问**前沿**——所有前提已定、此刻能诚实提问的问题，并且**每个问题都带推荐答案**，你可以直接按编号回答：

```
❓ **Q1 —— 目标用户是谁**：你说的「给开发者用」，指个人开发者还是团队？这决定后面定价与协作功能的取舍。

➡️ 我倾向「个人开发者优先」。理由：团队决策链长，与你「两周内上线验证」的时间约束冲突。

---

❓ **Q2 —— 成功标准**：「验证成功」是可验证判据，还是主观判断？

➡️ 建议定为「两周内 20 个真实用户走完一次完整任务」。理由是它可观测，且不依赖你的判断。
```

两条硬规则：

- **事实归它，决策归你。** 凡是环境、文件、网络能查到的事实，它自己查或派子代理去查，绝不拿来问你；只有目标、约束、取舍、口味这些**属于用户的决策**才会摆到你面前并等你回答。它不会自问自答你的决策。
- **前沿为空 ≠ 可以开工。** 访谈结束的标志是问题问完**且你明确确认理解一致**，在此之前它不会交成品。

### 落实：产出可执行文档

问题定义 → 方案空间与权衡 → 推荐路径 → 里程碑（含验收标准）→ 风险与对策 → 下一步最小行动。落到工作目录的 `idea/` 下。

### 推进：跨会话接着走

新会话先读已有文档与目标状态，接着上次的进度继续，不重复已经定过的决策，并定期复盘：什么变了／哪个假设被推翻／哪个方向该放弃。

## 内置技能

三个技能随 preset 一起分发（放在 `idea-forge/skills/`，通过 `customSkillDirs` 加载），按需自动加载：

| 技能 | 作用 |
|---|---|
| `idea-grilling` | 完整访谈协议：决策树／前沿／轮次、问题格式、反模式、停止信号 |
| `idea-divergence` | 发散技法（SCAMPER、反向头脑风暴、约束移除）与收敛评估（评估矩阵、pre-mortem、二阶效应、可逆性分类） |
| `idea-artifacts` | 产出物规范：方案骨架、术语表、决策记录三条件、进展日志 |

## 工具集

| 保留 | 移除 |
|---|---|
| 文件读写与检索、联网搜索与抓取、goal 目标、计划模式、todo、ask-user、子代理（spawn/fork）、后台任务、压缩 | Shell（bash/pwsh）、workflow、ralph |

## 设计依据

三处刻意的设计选择：

**1. 访谈协议同时写在 persona 和技能里。** 上游项目自己的文档记录了「命名另一个 skill 的 skill 不会可靠地触发加载」这一未修复问题，所以协议骨架必须能独立成立——即使技能一次都没被加载，行为也已经可用；技能只负责深度。

**2. 框架按机制分派，不按习惯堆叠。** 默认答案是「不用框架，直接推理」；只有机制正好对上才用，最多叠加 3 个且每个必须负责独立问题。同义框架不许叠加（例如「反转」已被 pre-mortem 吸收）。

**3. 每个技能都带非触发边界。** 任务小且可撤、用户只要一个事实、用户已拍板你只是落实——这些情况不走访谈流程。缺了这条，方法论会退化成仪式。

### 关于证据的诚实说明

这类「思维框架技能」的**实证支持很弱**。[tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) 做过一份少见的自省式审计：它最好的一条方向性结果是 scientific-method **+4.0pp**，**低于作者自设的 +5pp 效用门槛**；socratic 为 **−6.9pp**（负面）；28 个技能中 14 个从未测量；作者因此把全部技能标记为**永不自动调用**。

本 preset **没有**引用那份审计来支持自己的有效性——它恰恰说明整个品类的证据不足。这里的选择依据是**设计理由**（消除隐含假设、把用户的决策成本压到最低），不是测量出来的提升。尤其访谈协议是提问式的，而上述基准测的是**无真人在环的模型任务正确率**——它既不能证明也不能否定这种协议，**它只是未经验证**。

## 仓库结构

```text
dsh-think-partner/          # 克隆下来的仓库目录
├── README.md
├── LICENSE
└── idea-forge/              # ← 这个目录就是 preset，复制它
    ├── preset.yml           # 名称与描述（选择器可见）
    ├── agent.cordis.yml     # 组成文件
    └── skills/
        ├── idea-grilling/SKILL.md
        ├── idea-divergence/SKILL.md
        └── idea-artifacts/SKILL.md
```

## 已知限制

- **只做过挂载校验。** `agentPresets.standingKeyFor()` 通过，说明组成可挂载、`customSkillDirs` 配置生效；但挂载校验**不列出技能**，三个技能是否出现在会话技能目录中，需要在真实会话里确认。
- **轮次式提问是有争议的默认值。** 上游实践者反馈：慢读者、非母语者、把逐题当专注脚手架的人更适合「一次问一题」。如果你更想要逐题节奏，改 persona 第四节即可。
- **面向中文交互编写。** persona 与技能均为中文。

## 许可与出处

MIT，见 [LICENSE](LICENSE)。

组成文件派生自 DeepSeek Harness 的 `standard` 预设（`@deepseek-ai/dsh-agent-presets`，MIT）；`skills/` 下的三个技能为本仓库原创。

机制灵感来源（**未复制其文本**）：

- [mattpocock/skills](https://github.com/mattpocock/skills) — 决策树／前沿／轮次的访谈协议、事实与决策的分工
- [johnlindquist/claude](https://github.com/johnlindquist/claude) — 发散技法与评估矩阵、pre-mortem／二阶效应／机会成本
- [tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) — 技能模板（触发／非触发边界／过程／校验）、机制吸收与去冗余、按机制分派的纪律
