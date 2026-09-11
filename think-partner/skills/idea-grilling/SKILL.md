---
name: idea-grilling
description: Use when an idea, plan or decision needs interrogating — run a relentless interview on a decision tree, a frontier and rounds until nothing is left silently assumed. Trigger phrases include "grill me", "help me pin this down", "I can't articulate this idea", and any refine phase that finds key decisions still unsettled.
---

# The grilling protocol

Goal: before anything is produced, force every silently assumed part of the idea out into the open.

The interview is finished **not** when "enough has been asked", but when **the frontier is empty and the user confirms shared understanding**.

## When to use / when not to

**Use** when: key decisions are still open; the user cannot articulate it themselves; the plan looks reasonable but nobody has checked its premises; the investment is large or hard to reverse.

**Do not use** when:

- The task is small, cheap and reversible — just do it, skip the ceremony.
- The user wants one fact or one execution step; no decision is open.
- The user has already decided and you are only implementing — asking now is stalling.
- You are listing questions to *look* rigorous. That is framework theatre. Stop.

**Stop signals** (wrap up rather than padding rounds): a whole round yields only rewordings of existing questions; or further questions only re-ask what is already settled.

## The three core concepts

- **Decision tree** — the idea as a tree: every decision branches into the decisions hanging off it. The root is usually "what problem is this actually solving".
- **Frontier** — every decision whose prerequisites are already settled: the only questions that can honestly be asked right now, without guessing at answers you have not heard.
- **Round** — one entire frontier, asked in full and answered in full.

## Round rules

1. A round contains only **mutually independent** questions. If question B depends on question A and A is still open this round, B belongs to a **later round**.
2. Ask the round, then stop. Wait for the answers before computing the next round. Do not tag on follow-ups or pre-load the next round.
3. After each round, recompute the frontier: settled decisions push it outward and unblock new questions.
4. Thirteen questions typically land in three rounds, not thirteen. **Many questions, few rounds.**
5. A question that needs a fact you do not have is not a question for the user. Suspend that branch and go find the fact (see below); only the questions downstream of it wait.

## Question format

Every question has the same three parts, so the user can answer by number ("1 yes, 2 the second option, 3 no because…"):

```
❓ **Q1 — <question title>**: <question body, may be several paragraphs, may include options>

➡️ <your recommended answer>
```

Separate questions with `---`.

The recommendation is mandatory. It does two jobs: it reduces the user's cost to agree-or-disagree, and it exposes your reasoning to inspection. If your recommendation contradicts the question as worded, say so explicitly — "literally the answer is *no*, because…" — never leave the user to guess.

## Facts are yours, decisions are the user's

- **Facts**: environment, files, directories, public data, competitor information, market numbers — all yours. Look them up with file and web tools, or dispatch a subagent. **Never ask the user something you could have discovered.**
- **Decisions**: goals, constraints, tradeoffs, taste, priorities — the user's. Put each one in front of them and **wait**.
- Answering the user's decisions for them is not "being flexible", it is **going off the rails**. Answering your own decisions voids the interview.

## Do not block on a single thing

Research still running does not count as settled, so **only the questions downstream of it** wait; the rest of the round goes out now. Never stall a whole round waiting for research to finish.

## Ending and the confirmation gate

- The interview ends when the **frontier is empty**: every branch visited, nothing silently assumed.
- An empty frontier is **not** permission to start. Explicitly ask the user to confirm you have reached shared understanding, and only then move to the realize phase.
- Until they confirm: no finished documents, no "final plan", no drifting into execution.

## Anti-patterns (any one means the run went wrong)

- **Giving a plan after two questions** — collapsing "interview until shared understanding" into "two questions and an outline" is the most common failure.
- **Answering your own questions for the user.**
- **Packing mutually dependent questions into one round** — the user cannot answer them in sequence.
- **Asking the user for facts you should have looked up.**
- **Questions with no recommendation** — that pushes the whole cost of deciding back onto the user.

## The honest limit

The frontier is your judgement, not a computed graph. You may put two questions in one round and only afterwards discover that one answer should have changed the other. Nothing prevents this — but when you notice, say so plainly ("this round's Q2 assumed something Q3 overturned") and reopen that branch in the next round.

## Self-check

- A round arrives as a numbered list, each question with its own `➡️` recommendation, answerable by number.
- Nothing in a round needs another question in the same round answered first.
- Later rounds ask what the first round could not have asked.
- Facts were looked up, not asked for.
- Background research did not stall the round.
- It stopped and asked for confirmation instead of starting work.
- High question count, low round count.
