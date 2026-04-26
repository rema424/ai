---
name: hi-fi-spike-decision
description: Use when deciding whether to continue incremental fixes on the current branch or reclassify it as a Hi-Fi Spike and restart from a clean base. Evaluates shipping context, regression patterns, design complexity, whiteboard-minimal design, total cost, and recommends A or B.
license: MIT
---

# Hi-Fi Spike Decision

Use this skill to decide whether the current branch should continue as incremental production work or be reclassified as a Hi-Fi Spike whose lessons feed a clean-room production implementation.

## Goal

Recommend exactly one of:

- **A. 追記型修正の継続**: Keep the current branch and continue fixing it toward shipment.
- **B. Hi-Fi Spike 化**: Treat the current branch as production-quality design exploration, extract lessons, then restart production implementation from a clean base branch.

Do not over-recommend B. If A is sufficient, recommend A clearly.

## Workflow

### 1. Fix the Shipping Context

Clarify:

- 出荷目的: demo / internal validation / production / merge-and-maintain
- 想定寿命: about 1 week / 1 month / 1 year+
- 後続変更: one-off / continued feature work

Guidance:

- demo, disposable, short-lived code favors A.
- production, long-lived, actively extended code favors B.

### 2. Compare Against a Whiteboard-Minimal Design

Before judging the current implementation, describe the simplest natural design that would satisfy the same requirement from a clean base:

- essential responsibility
- authoritative source
- contract / API / type / protocol boundaries
- state machine and invariants
- minimal modules / components / APIs / state
- data flow that avoids duplicate truth

Then compare the current branch against that design:

- Is the current implementation larger than the feature's essential complexity?
- Are there accidental branches, duplicate state, adapters, conversions, sync paths, or corrective logic?
- Did previous fixes become central to the design?
- Are frontend, backend, cache, tests, or optimistic UI compensating for unclear contracts?
- Could the same requirement be served by fewer concepts and a clearer data flow?

Complexity signals:

- implementation volume is high relative to the actual feature
- same concept is represented in multiple places or shapes
- state synchronization, exception branches, or correction logic dominate
- API contract gaps are covered by UI or tests
- responsibility is scattered across modules
- code cannot explain why a fix is necessary without historical context
- a clean-room version would clearly be smaller

Three or more signals favor B. One or two signals keep A viable. Zero signals favor A.

### 3. Analyze Failure and Regression Patterns

Inspect recent commits, diffs, review comments, test failures, or user-reported reversions as available.

Answer:

- How many recent reversions or fix rounds exist?
- Are they independent, or do they share a common root?
- If common, state the root in one sentence.
- How many times did "fix A breaks/reopens B" occur?
- Are regressions accidental, or caused by coupling, unclear contracts, scattered state, or duplicate truth?

Design problem signals:

- backend truth and frontend assumptions diverge
- authoritative source is unclear
- optimistic UI compensates for missing API guarantees
- contract or state machine is being discovered after implementation
- the same area has been edited repeatedly
- fix-break-fix loops are visible

Three or more signals favor B. One or two signals keep A viable. Zero signals favor A.

### 4. Compare Total Cost

Estimate A and B in the same unit: sessions, hours, or remaining work rounds.

For A, include:

- known remaining fixes
- likely new regressions from touching the same areas
- estimated stabilization rounds
- future maintenance cost of current complexity

For B, include:

- lesson extraction and handoff cost
- clean-room implementation cost using spike lessons
- reusable test intent and acceptance criteria
- future maintenance cost saved by simpler design

Compare:

- cost to ship this change
- cost of the next similar change
- regression risk
- cognitive load
- ease of review, explanation, and handoff

## Output Format

Use this structure:

```markdown
## 推奨: A / B

### 確認できた事実

- ...

### 推測

- ...

### 白紙設計観点での評価

- 最小設計:
- 現在実装との差分:
- 削れる複雑性:

### 根拠

1. ...
2. ...
3. ...

### コスト比較

| 方針 | 見積もり | 主なコスト | 主なリスク |
| --- | --- | --- | --- |
| A | ... | ... | ... |
| B | ... | ... | ... |

### 反対の立場からの検討

- もし A を選ぶなら:
- もし B を選ぶなら:

### 最終判断

...
```

If recommending B, also list:

- assets to preserve: test intent, structural lessons, regression patterns, API/state/UX decisions
- assets to discard: accidental branches, local fix complexity, unnecessary state/conversion/sync paths
- likely base branch for clean-room implementation

## Stop and Ask

Ask the user before deciding if:

- shipping purpose or base branch cannot be inferred
- the working tree does not contain enough history or diffs to evaluate failure patterns
- the recommendation depends on product priority rather than engineering cost
