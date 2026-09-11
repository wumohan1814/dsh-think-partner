# dsh-think-partner

**A structured thinking partner for DeepSeek Harness.** Turn a vague idea into a decision-complete plan — then keep moving it forward. No code required.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Platform: DeepSeek Harness](https://img.shields.io/badge/platform-DeepSeek%20Harness-000000.svg)](https://github.com/deepseek-ai/deepseek-harness)
[![Type: agent preset](https://img.shields.io/badge/type-agent%20preset-6f42c1.svg)](#what-it-is)
[![Editions: EN + 中文](https://img.shields.io/badge/editions-EN%20%2B%20%E4%B8%AD%E6%96%87-2ea44f.svg)](#two-editions)
[![Skills: 3](https://img.shields.io/badge/skills-3-2ea44f.svg)](#built-in-skills)
[![GitHub stars](https://img.shields.io/github/stars/wumohan1814/dsh-think-partner?style=social)](https://github.com/wumohan1814/dsh-think-partner/stargazers)

> Not another "let's brainstorm!" prompt. This is an agent preset that interrogates your idea the way a good technical co-founder would — one round of pointed questions at a time, each with a recommended answer, until nothing is left silently assumed.

**English** · [中文文档](#中文文档)

---

## Table of contents

- [What it is](#what-it-is)
- [Two editions](#two-editions)
- [Why it's different](#why-its-different)
- [See it work](#see-it-work)
- [Quick start](#quick-start)
- [The workflow: refine → realize → advance](#the-workflow-refine--realize--advance)
- [Built-in skills](#built-in-skills)
- [Tools](#tools)
- [Design notes](#design-notes)
- [On evidence — please read](#on-evidence--please-read)
- [Repository layout](#repository-layout)
- [Known limitations](#known-limitations)
- [License & credits](#license--credits)

## What it is

`dsh-think-partner` is an **agent preset** for [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) (DSH). In DSH, every capability is a plugin row in a `cordis.yml`, and an agent preset decides which tools and prompt sections one session gets.

This preset is built for exactly one job: **thinking an idea through** — refining it, making it concrete, and advancing it across many sessions.

It is deliberately **not** a coding agent. Shell, workflow orchestration and build tooling are all removed. What's left is a thinking partner with memory: file tools to write documents, web access to check facts, goals to keep long-running ideas alive across sessions, and subagents to delegate research.

**Keywords:** DeepSeek Harness preset · structured reasoning · thinking partner · idea validation · decision tree · requirement elicitation · pre-mortem · second-order effects · agent skills.

## Two editions

| Edition | Directory | Preset id | Persona & skills | Name in the picker |
|---|---|---|---|---|
| **English** | [`think-partner/`](think-partner/) | `think-partner` | English | **Think Partner** |
| **Chinese** | [`idea-forge/`](idea-forge/) | `idea-forge` | Chinese | **Think Partner 中文版** |

The two editions are **functionally identical** — same tools, same interview protocol, same three skills. Only the language of the persona and the method documents differs. Install one, or both; they don't conflict.

In this README, "the preset" means whichever edition you installed.

## Why it's different

Three things separate this from "You are a helpful brainstorming assistant."

**1. It interrogates instead of agreeing.**
Your idea becomes a **decision tree**. Each round asks only the **frontier** — the questions whose prerequisites are already settled, and nothing else — and **every question ships with a recommended answer**, so you can reply by number:

```
1 yes · 2 option B · 3 no, because…
```

Thirteen questions land in about three rounds, not thirteen. Two questions never share a round if one depends on the other.

**2. Facts are its job. Decisions are yours.**
If an answer is discoverable — in your files, on the web, in a competitor's pricing page — it goes and finds it, or dispatches a subagent, instead of asking you. Only what is genuinely *yours* — goals, constraints, tradeoffs, taste — comes back as a question. And it does not answer your decisions for you; an agent that does has stopped running this protocol.

**3. Nothing gets built before you confirm.**
The interview ends when the frontier is empty **and** you explicitly confirm you're on the same page. Until then: no "final plan", no documents, no drift into execution.

## See it work

A real round looks like this — numbered, each with its recommendation, answerable in one line:

```
❓ Q1 — Who is the target user: individual developers or teams?
   This decides pricing and whether collaboration features matter.

➡️ I'd go individual-developer-first. Teams have longer decision chains,
   which conflicts with your "validate in two weeks" constraint.

---

❓ Q2 — Is "validated" a measurable criterion or a gut call?

➡️ Make it "20 real users complete one full task within two weeks".
   It's observable and doesn't depend on your judgement.
```

You answer `1 agree, 2 yes but make it 10 users, 3 ...` and the next round is computed from your answers.

## Quick start

```powershell
# 1. Clone
git clone https://github.com/wumohan1814/dsh-think-partner.git dsh-think-partner

# 2. Copy the edition you want into your DSH preset root
Copy-Item -Recurse dsh-think-partner\think-partner "$env:USERPROFILE\.dsh\.agent-presets\"   # English

Copy-Item -Recurse dsh-think-partner\idea-forge "$env:USERPROFILE\.dsh\.agent-presets\"      # Chinese (optional)
```

The preset root is `${DSH_HOME:-$HOME/.dsh}/.agent-presets/` — adjust if you set `DSH_HOME`.

Then restart DSH and pick **Think Partner** (or **Think Partner 中文版**) in the preset picker. That's it: no config, no commands, no code.

> A preset's id comes from its directory name, so the two directories must keep the names `think-partner` and `idea-forge`. They are independent of this repository's name.

## The workflow: refine → realize → advance

**Refine** — run the interview protocol above, and collapse fuzzy or overloaded wording into precise definitions the moment you hit it. ("You're saying *user* — do you mean the paying customer or the end user? Those are different things.")

**Realize** — produce an executable document: problem definition → solution space and tradeoffs → recommended path → milestones *with acceptance criteria* → risks and mitigations → the next minimal action. Written to `idea/` in your working directory.

**Advance** — a new session starts by reading the existing documents and goal state, picks up where you left off, and never re-asks a settled decision. Periodic review asks the three questions that matter: *What changed? Which assumption died? Which direction should we drop?*

## Built-in skills

Three skills ship **inside each preset** (loaded via `customSkillDirs`) and load on demand:

| Skill | What it does |
|---|---|
| `idea-grilling` | The full interview protocol: decision tree, frontier, rounds, question format, anti-patterns, stop signals |
| `idea-divergence` | Divergent techniques (SCAMPER, reverse brainstorming, constraint removal) and convergent evaluation (scoring matrix, pre-mortem, second-order effects, reversibility triage) |
| `idea-artifacts` | Document conventions: plan skeleton, glossary, decision records (the three-condition ADR test), progress log |

## Tools

| Kept | Removed |
|---|---|
| File read/write/search, web search & fetch, goals, plan mode, todos, ask-user, subagents (spawn/fork), background jobs, compaction | Shell (bash/pwsh), workflow, ralph |

## Design notes

**The interview protocol lives in both the persona and the skills.** Upstream projects document that a skill naming another skill does not reliably cause it to load. So the non-negotiable rules sit in the persona and the depth sits in the skills — if a skill never loads, the behaviour still holds.

**Frameworks are dispatched by mechanism, not stacked by habit.** The default answer is "no framework, just reason". A framework is used only when its mechanism matches the problem, at most three at a time, each answering a question the others don't. Near-synonyms never stack — inversion has been absorbed into pre-mortem, so it isn't counted twice.

**Every skill carries a non-trigger boundary.** Small and reversible task, a user who just wants one fact, a decision already made — these don't get the interview treatment. Without that boundary, methodology degrades into ritual.

## On evidence — please read

Thinking-framework skills have **weak empirical support**, and this repository won't pretend otherwise. [tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) published an unusually self-critical audit of its own catalog: its best directional result (scientific-method) was **+4.0pp — below the author's own +5pp utility margin**; socratic scoring was **−6.9pp (negative)**; 14 of 28 skills were never measured. The author consequently marked every skill manual-only and never auto-invoked.

This preset does **not** cite that audit as support for its own effectiveness — it demonstrates that the whole category is under-evidenced. The justification here is a **design rationale** (removing silent assumptions, making the user's decisions cheap), not a measured lift. The interview protocol in particular is question-based, while those benchmarks measure model task accuracy **with no human in the loop** — they neither validate nor invalidate it. **It is simply untested.**

## Repository layout

```text
dsh-think-partner/
├── README.md
├── LICENSE
├── think-partner/          # ← English edition; copy this directory
│   ├── preset.yml          # name & description (shown in the picker)
│   ├── agent.cordis.yml    # the composition
│   └── skills/
│       ├── idea-grilling/SKILL.md
│       ├── idea-divergence/SKILL.md
│       └── idea-artifacts/SKILL.md
└── idea-forge/             # ← Chinese edition; copy this directory
    ├── preset.yml
    ├── agent.cordis.yml
    └── skills/
        ├── idea-grilling/SKILL.md
        ├── idea-divergence/SKILL.md
        └── idea-artifacts/SKILL.md
```

## Known limitations

- **Mount-validated only.** `agentPresets.standingKeyFor()` passes for both editions, which proves the compositions mount and the `customSkillDirs` config takes effect. It does **not** list skills, so whether the three skills appear in a session's skill catalog still needs confirming in a real session.
- **Round-based questioning is a contested default.** Practitioners who read slowly, work in a second language, or use one-question-at-a-time as focus scaffolding often prefer sequential. Edit section 4 of the persona if that's you.
- **The two editions can drift.** They are maintained as parallel copies; fixes must be applied to both.

## License & credits

MIT — see [LICENSE](LICENSE).

The compositions derive from DeepSeek Harness's `standard` preset (`@deepseek-ai/dsh-agent-presets`, MIT). The skills in both editions are original to this repository.

Mechanisms were inspired by — **without copying any text from** — these projects:

- [mattpocock/skills](https://github.com/mattpocock/skills) — the decision-tree / frontier / round interview protocol, and the facts-vs-decisions split
- [johnlindquist/claude](https://github.com/johnlindquist/claude) — divergent techniques, evaluation matrices, pre-mortem / second-order / opportunity cost
- [tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) — the skill template (trigger / non-trigger boundary / procedure / checks), mechanism absorption, and mechanism-fit dispatch

If this is useful to you, a ⭐ helps other people find it.

---

# 中文文档

**给 DeepSeek Harness 用的结构化思考搭档。** 把一个模糊的想法，变成决策完备的方案，然后持续推进它。不需要写代码。

> 不是又一个「我们来头脑风暴吧」的提示词。这是一个 agent preset：它像一位好的技术合伙人那样拷问你的想法——每轮只问一组有指向性的问题，每个问题都附带推荐答案，直到没有东西被默默假设掉。

## 它是什么

`dsh-think-partner` 是 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)（DSH）的 **agent preset**。在 DSH 里，每一项能力都是 `cordis.yml` 中的一行插件，而一个 agent preset 决定一个会话拿到哪些工具与提示词段落。

这个 preset 只为一个任务而建：**把想法想透**——细化它、落实它、并跨多个会话推进它。

它刻意**不是**编码 Agent：Shell、workflow 编排、构建工具全部移除。留下的是一个有记忆的思考搭档——文件工具用来写文档，联网用来查证事实，goal 目标让长期想法跨会话存活，子代理用来委派调研。

## 两个版本

| 版本 | 目录 | preset id | persona 与技能 | 选择器里的名称 |
|---|---|---|---|---|
| **英文版** | [`think-partner/`](think-partner/) | `think-partner` | 英文 | **Think Partner** |
| **中文版** | [`idea-forge/`](idea-forge/) | `idea-forge` | 中文 | **Think Partner 中文版** |

两个版本**功能完全一致**——相同的工具、相同的访谈协议、相同的三个技能，只有 persona 与方法论文档的语言不同。可以只装一个，也可以都装，它们不冲突。

## 它凭什么不一样

**1. 它拷问你，而不是附和你。**
你的想法会被建成一棵**决策树**。每轮只问**前沿**——所有前提已定、此刻能诚实提问的问题——并且**每个问题都附推荐答案**，你可以直接按编号回答：

```
1 同意 · 2 选第二个 · 3 不，因为…
```

13 个问题通常落成 3 轮，而不是 13 轮。只要两个问题互相依赖，它们绝不会出现在同一轮。

**2. 事实归它，决策归你。**
凡是能查到的——你的文件里、网上、竞品的定价页——它自己去查，或派子代理去查，而不是拿来问你。只有真正**属于你**的：目标、约束、取舍、口味，才会作为问题回到你面前。它也不会替你拍板；一旦替用户回答决策，这个协议就已经失效了。

**3. 你没确认之前，什么都不产出。**
访谈结束的条件是前沿为空，**并且**你明确确认双方理解一致。在那之前：没有「最终方案」，没有成品文档，也不会悄悄滑进执行。

## 快速上手

```powershell
# 1. 克隆
git clone https://github.com/wumohan1814/dsh-think-partner.git dsh-think-partner

# 2. 把你要的版本复制进 DSH 的用户预设根目录
Copy-Item -Recurse dsh-think-partner\idea-forge "$env:USERPROFILE\.dsh\.agent-presets\"      # 中文版

Copy-Item -Recurse dsh-think-partner\think-partner "$env:USERPROFILE\.dsh\.agent-presets\"   # 英文版（可选）
```

预设根目录是 `${DSH_HOME:-$HOME/.dsh}/.agent-presets/`，设置过 `DSH_HOME` 请相应替换。

重启 DSH，在预设选择器里选 **Think Partner 中文版**（或 **Think Partner**）。就这样：不需要配置、不需要命令、不需要代码。

> preset 的 id 取自目录名，所以两个目录必须保持叫 `think-partner` 与 `idea-forge`。它们与仓库名无关。

## 工作循环：细化 → 落实 → 推进

**细化** —— 跑上面那套访谈协议；遇到含糊或一词多义的措辞，当场收敛成精确定义。（「你说的*用户*，指付费客户还是最终使用者？这是两个东西。」）

**落实** —— 产出可执行文档：问题定义 → 方案空间与权衡 → 推荐路径 → 里程碑（**含验收标准**）→ 风险与对策 → 下一步最小行动。写到工作目录的 `idea/` 下。

**推进** —— 新会话先读已有文档与目标状态，接着上次继续，绝不重复追问已经定过的决策。定期复盘只问三个要紧的问题：*什么变了？哪个假设死了？哪个方向该放弃？*

## 内置技能

三个技能**随每个版本一起分发**（通过 `customSkillDirs` 加载），按需加载：

| 技能 | 作用 |
|---|---|
| `idea-grilling` | 完整访谈协议：决策树、前沿、轮次、问题格式、反模式、停止信号 |
| `idea-divergence` | 发散技法（SCAMPER、反向头脑风暴、约束移除）与收敛评估（评分矩阵、pre-mortem、二阶效应、可逆性分类） |
| `idea-artifacts` | 产出物规范：方案骨架、术语表、决策记录（三条件 ADR 判定）、进展日志 |

## 工具集

| 保留 | 移除 |
|---|---|
| 文件读写与检索、联网搜索与抓取、goal 目标、计划模式、todo、ask-user、子代理（spawn/fork）、后台任务、压缩 | Shell（bash/pwsh）、workflow、ralph |

## 设计说明

**访谈协议同时写在 persona 和技能里。** 上游项目自己的文档记录了「命名另一个 skill 的 skill 不会可靠地触发加载」这一未修复问题。所以不可让步的规则放在 persona，深度放在技能——即使技能一次都没加载，行为依然成立。

**框架按机制分派，不按习惯堆叠。** 默认答案是「不用框架，直接推理」。只有当框架的机制正好对上问题才用，最多 3 个，且每个负责其他框架覆盖不到的独立问题。同义框架不许叠加——反转已被 pre-mortem 吸收，不重复计数。

**每个技能都带非触发边界。** 任务小且可撤、用户只要一个事实、决策已经拍板——这些情况不走访谈流程。缺了这条，方法论会退化成仪式。

## 关于证据，请务必读这一段

思维框架类技能的**实证支持很弱**，本仓库不会假装不是。[tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) 对自己那份目录做过一次少见的自省式审计：它最好的一条方向性结果（scientific-method）是 **+4.0pp，低于作者自设的 +5pp 效用门槛**；socratic 为 **−6.9pp（负面）**；28 个技能中 14 个从未测量。作者因此把全部技能标记为永不自动调用。

本 preset **没有**引用那份审计来支持自己的有效性——它恰恰说明整个品类的证据都不足。这里的选择依据是**设计理由**（消除隐含假设、把用户的决策成本压到最低），不是测量出来的提升。尤其访谈协议是提问式的，而那些基准测的是**无真人在环**的模型任务正确率——既不能证明也不能否定它。**它只是未经验证。**

## 仓库结构

```text
dsh-think-partner/
├── README.md
├── LICENSE
├── think-partner/          # ← 英文版；复制这个目录
│   ├── preset.yml          # 名称与描述（选择器可见）
│   ├── agent.cordis.yml    # 组成文件
│   └── skills/
│       ├── idea-grilling/SKILL.md
│       ├── idea-divergence/SKILL.md
│       └── idea-artifacts/SKILL.md
└── idea-forge/             # ← 中文版；复制这个目录
    ├── preset.yml
    ├── agent.cordis.yml
    └── skills/
        ├── idea-grilling/SKILL.md
        ├── idea-divergence/SKILL.md
        └── idea-artifacts/SKILL.md
```

## 已知限制

- **只做过挂载校验。** 两个版本的 `agentPresets.standingKeyFor()` 都通过，证明组成可挂载、`customSkillDirs` 配置生效；但它**不列出技能**，所以三个技能是否真的出现在会话技能目录里，仍需在真实会话中确认。
- **轮次式提问是有争议的默认值。** 慢读者、非母语者、把逐题当专注脚手架的人，往往更适合一次问一题。如果你属于这类，改 persona 第四节即可。
- **两个版本会各自漂移。** 它们是并行维护的两份拷贝，任何修订都要同时改两边。

## 许可与出处

MIT，见 [LICENSE](LICENSE)。

组成派生自 DeepSeek Harness 的 `standard` 预设（`@deepseek-ai/dsh-agent-presets`，MIT）。两个版本中的技能均为本仓库原创。

机制灵感来源（**未复制其任何文本**）：

- [mattpocock/skills](https://github.com/mattpocock/skills) —— 决策树／前沿／轮次的访谈协议、事实与决策的分工
- [johnlindquist/claude](https://github.com/johnlindquist/claude) —— 发散技法、评估矩阵、pre-mortem／二阶效应／机会成本
- [tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) —— 技能模板（触发／非触发边界／过程／校验）、机制吸收、按机制分派

如果它对你有用，点个 ⭐ 能让更多人找到它。
