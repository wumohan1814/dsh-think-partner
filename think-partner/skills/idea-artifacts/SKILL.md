---
name: idea-artifacts
description: Use when an idea must be written down — plan skeleton, glossary of precise definitions, decision records (the three-condition ADR test), milestones with acceptance criteria, progress log and retros. Triggers include writing a plan, spec or proposal, defining terminology, recording an important decision, updating progress, and phrases like "write it up", "save this", "make it concrete".
---

# Artifact conventions

The files in the working directory are this idea's **long-term memory**, and the only basis for "advance" across sessions. Create them on demand — never generate a pile of empty files up front.

```
idea/
├── README.md        # one page: what this is, where it stands, what's next
├── plan.md          # problem → solution space → path → milestones → risks
├── glossary.md      # definitions only, no implementation detail
├── decisions/       # 0001-xxx.md, only decisions worth recording
└── log.md           # one line per advance: date / did / learned / next
```

**When not to use**: one-off Q&A, a user who only wants a verbal answer, or an idea so early that the problem itself is not yet defined — writing documents then is a liability, not an asset. Files are for things that will keep moving.

**Done test**: someone who never saw this conversation can read the documents and know what to do next. If not, the documents are talking to themselves.

## 1. Tighten the language before discussing the plan

A vague idea is usually a vague **word**. When the refine phase hits any of these, collapse it on the spot — never batch it for later:

- **One word, two meanings** — "user": the paying customer or the end user? Those are different things; separate them first.
- **Conflicts with the glossary** — the glossary defines "cancellation" as X, but you seem to mean Y. Which is it?
- **Vague degree words** — "fast", "cheap", "at scale": replace with a number or a checkable criterion.
- **One thing, two names** — decide which is canonical and record the other as an alias.

Write the result into `glossary.md` **immediately**. The glossary holds **definitions only** — it is not a spec, not a scratchpad, and it carries no implementation detail.

## 2. Stress-test boundaries with concrete scenarios

Relationships between concepts cannot be pinned down in the abstract. **Invent extreme scenarios** yourself and force the boundaries out:

What if someone refunds mid-way? What if two people want the same slot? What about empty, enormous or duplicate input? What if the order is reversed?

The point is not to answer them, but to force the user to take a position on **where the line between concepts sits**.

## 3. Decision records: write one only when all three hold

1. **Hard to reverse** — changing your mind later has a real cost.
2. **Surprising without context** — a future reader will ask "why on earth was it done this way?"
3. **The result of a real tradeoff** — genuine alternatives existed and you chose this one for specific reasons.

If any of the three is missing, **do not write it** — otherwise the decisions directory degrades into noise.

At minimum record: context / alternatives / decision / reasoning / cost and impact / **what would make you revisit it**.

## 4. Plan skeleton (plan.md)

- **Problem definition** — for whom, solving what, and **what it does not solve** (the boundary matters just as much).
- **Success criteria** — checkable criteria, not adjectives.
- **Solution space and tradeoffs** — at least 2–3 alternatives and what each costs.
- **Recommended path** — which one, why, and what it gives up.
- **Milestones** — each with a **deliverable and acceptance criteria**, concrete enough to start immediately.
- **Risks and mitigations** — the list produced by pre-mortem and reverse brainstorming.
- **Next minimal action** — one at a time, and verifiable.

## 5. Progress log and retro (log.md)

- One line per advance: date / what was done / what was learned / next.
- Periodic retro asks three questions: **what changed? which assumption died? which direction should be dropped?**
- When the plan changes, go back and edit the recommended path in `plan.md` — do not let direction drift silently in a chat log.

## 6. Session opening move

At the start of a new session, read `idea/README.md` first (if there is none, start from scratch), then `plan.md` and `log.md` as needed, and **continue from where the last session stopped rather than re-asking settled decisions**. If the documents contradict what you now believe, say so — never quietly pick a side.
