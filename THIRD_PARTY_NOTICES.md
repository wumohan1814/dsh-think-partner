# Third-party notices

This repository contains material derived from third-party projects. Below is
what was taken from each, and the license notices that those licenses require to
be preserved. The MIT texts are reproduced in full.

If anything here is attributed incorrectly, please open an issue and it will be
corrected.

---

## 1. DeepSeek Harness — MIT

**Applies to:** `think-partner/agent.cordis.yml`, `idea-forge/agent.cordis.yml`

Both compositions are derived from the `standard` agent preset that ships with
DeepSeek Harness (npm package `@deepseek-ai/dsh-agent-presets`). The plugin rows,
their configuration, part of the commentary and the plan-mode prompt section are
adapted from it. The personas and the three skills are original to this
repository.

- Source: <https://github.com/deepseek-ai/deepseek-harness>
- License: MIT

```text
MIT License

Copyright (c) 2026 DeepSeek

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 2. mattpocock/skills — MIT

**Applies to:** `think-partner/skills/idea-grilling/SKILL.md`,
`idea-forge/skills/idea-grilling/SKILL.md`

The grilling protocol is **adapted from** the `grilling` skill in
mattpocock/skills. Taken from it: the decision-tree / frontier / round model, the
numbered-question-plus-recommendation format, the facts-versus-decisions split,
the "thirteen questions land in about three rounds" framing, and the
confirmation gate before acting. Written for this repository: the when-not-to-use
boundaries, stop signals, anti-pattern list, honest-limits section and
self-check.

- Source: <https://github.com/mattpocock/skills>
- License: MIT

```text
MIT License

Copyright (c) 2026 Matt Pocock

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 3. tjboudreaux/cc-thinking-skills — MIT

**Applies to:** the document structure of all three skills, and the
framework-dispatch rules in both personas.

Taken from it: the skill document template (a precise trigger, a non-trigger
boundary, a procedure, and checks); the practice of recording which mechanism
absorbs which (for example inversion being absorbed into pre-mortem); and the
"route by mechanism fit, not habit" dispatch discipline, including the cap on
how many frameworks may be combined.

- Source: <https://github.com/tjboudreaux/cc-thinking-skills>
- License: MIT

```text
MIT License

Copyright (c) 2025 TJ Boudreaux

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 4. johnlindquist/claude — **no license granted**

**Applies to:** the technique list in `idea-divergence` only.

Taken from it: the set of named techniques (SCAMPER, Six Thinking Hats, reverse
brainstorming, constraint removal, a feasibility/impact/effort/risk scoring
matrix, pre-mortem, second-order effects, opportunity cost), plus three short
functional phrases — "steel man the counterargument", "what evidence would
change your mind?", and the proceed/modify/abandon decision.

**These are pre-existing public frameworks** (SCAMPER dates to 1971, Six Thinking
Hats and pre-mortem are likewise established techniques), and short functional
phrases are not individually protectable. **No document text was copied**: that
repository's skill files are shell-command templates, none of which appear here.
It is credited because it is where these were encountered while researching this
preset, and that debt is real.

That repository declares **no license**, so all rights are reserved by its
author. If the author objects to this credit, or believes more was taken than
described above, contact the maintainer and the relevant material will be
removed or rewritten.

- Source: <https://github.com/johnlindquist/claude>
- License: none declared
