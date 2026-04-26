---
name: spiral-autonomy
description: Use when Codex should run a learning-driven spiral process for ambiguous or evolving work across research, business planning, product planning, requirements, design, implementation, testing, or review. Triggers include requests for autonomous execution, high-agency planning, iterative discovery, hypothesis-driven work, upstream revision after implementation findings, subagent coordination, or maximizing learning from investigation/prototyping.
license: MIT
---

# Spiral Autonomy

## Operating Model

Run the task as a spiral process: treat the initial request as a provisional hypothesis, increase resolution through investigation or execution, and revise upstream assumptions when evidence changes.

Use a thin profile for the task type. If the user names a profile, use it. Otherwise infer one from the request. Switch profiles during the work when learning changes the needed phase.

- `research`: facts, sources, claims, uncertainty, implications.
- `business-plan`: customer, problem, market, economics, GTM, risks.
- `product-planning`: users, jobs, value, scope, roadmap, tradeoffs.
- `requirements`: stakeholders, use cases, requirements, constraints, acceptance criteria.
- `design`: alternatives, chosen design, rejected options, boundaries, operations, tests.
- `implementation`: scoped code changes, tests, review, integration.
- `review`: findings first, severity, evidence, residual risk.

For profile-specific output shapes, read `references/profiles.md` only when needed.

For requests that span discovery through planning, requirements, design, spike validation, and revision in one session, run a multi-phase spiral. Read `references/multi-phase.md` when the task asks for end-to-end autonomous execution, "from research to design", concept-to-design, product discovery, or spike-driven validation.

## Start

Begin by stating the user's objective and the first move in one or two sentences.

Then build a compact working frame:

- Provisional objective
- Known facts
- Assumptions
- Open questions
- Current profile
- Phase sequence, if multi-phase
- First cycle goal
- Completion criteria
- Checkpoint policy

If working in a repository, inspect local operating assets first: `AGENTS.md`, `.codex/`, README, CI/workflows, package manifests, task runners, and relevant docs. Prefer repo instructions over generic defaults.

## Delegation

Use subagents only when the user explicitly permits subagents, delegation, or parallel agent work.

When delegating:

- Keep the critical path local.
- Delegate bounded sidecar work that can run in parallel.
- Assign each subagent a concrete output, not a search task.
- Give each implementation subagent an explicit write scope.
- Tell workers they are not alone in the codebase and must not revert others' changes.
- Separate implementation and review when practical.
- Do not use subagents as generic search engines.

Good delegated outputs include: evidence table, design option with tradeoffs, scoped patch, test result analysis, risk review, acceptance criteria critique, or market hypothesis critique.

## Spiral Cycle

Run one or more cycles. Keep cycles small enough that learning can change direction before large sunk cost accumulates.

Each cycle:

1. State the hypothesis or question.
2. Gather only the context needed for the next decision.
3. Produce a small artifact: analysis, design, prototype, patch, test, review, or decision record.
4. Verify using the strongest practical method for the profile.
5. Extract learning.
6. Update upstream artifacts: objective, requirements, design, plan, acceptance criteria, or task split.
7. Decide whether to continue, stop, or ask for human judgment.
8. Decide whether to place a checkpoint.

Prefer evidence over momentum. If implementation reveals the premise is wrong, revise requirements or design before continuing implementation.

## Multi-Phase Work

When the user's goal spans multiple upstream phases, do not force a linear waterfall. Treat each phase output as a provisional artifact that can be revised by later evidence.

Default phase sequence:

1. Research: establish facts, constraints, and uncertainty.
2. Product or business planning: frame value, users/customers, scope, and strategy.
3. Requirements: define testable needs, constraints, and acceptance criteria.
4. Design: evaluate alternatives and choose a coherent approach.
5. Spike validation: run the smallest practical experiment, prototype, code spike, benchmark, model, or source check that can reduce the highest-risk uncertainty.
6. Revision: update research conclusions, plan, requirements, and design based on spike evidence.
7. Handoff: produce the next executable plan or decision package.

Move backward whenever later evidence invalidates earlier assumptions. Record what changed and why. Do not preserve an earlier plan merely for consistency.

Use spikes for high-risk assumptions, unclear feasibility, unknown integration behavior, UX/workflow ambiguity, performance uncertainty, data availability, cost assumptions, market/channel assumptions, or requirements that are difficult to make testable.

## Checkpoints

Use checkpoints to preserve evidence of learning and decision state. A checkpoint may be a git commit, a decision record, an updated requirements/design document, a saved plan, or a test artifact summary.

Default checkpoint policy:

- For long-running autonomous work in a git repository: use `auto-commit with limits` unless the user says not to commit.
- For short tasks, non-repository work, or analysis-only work: use `recommend-only` unless the user asks for commits.
- For production-impacting, destructive, secret-bearing, or unclear ownership work: use `disabled` until the user explicitly approves.

State the chosen checkpoint policy once near the start. Do not make the user repeat checkpoint instructions in the prompt.

Consider a checkpoint when:

- A cycle changes requirements, design, scope, or risk understanding.
- A coherent artifact is completed.
- A patch is working and verified before a riskier next step.
- A review finds material issues that should be preserved.
- Human approval or handoff is needed.

When using git commits:

- Do not ask for every checkpoint commit under `auto-commit with limits`; commit at meaningful cycle boundaries and report the list at the end.
- Ask before the first checkpoint commit only when the policy is not already `auto-commit with limits`.
- Keep one checkpoint to one logical change.
- Do not use `git add .`; stage only relevant files.
- Do not commit unrelated user changes.
- Use the repo's commit convention; otherwise prefer Conventional Commits.
- Include evidence in the message when useful: cycle purpose, verification, and issue/reference.
- Pause before committing if the commit would include secrets, credentials, destructive operations, production-impacting changes, or unrelated dirty worktree changes.
- If the worktree is already dirty, inspect it before starting and keep checkpoint commits limited to files changed for the current task.

Do not create noisy checkpoints for every minor edit. If no durable artifact changed, summarize the learning log instead.

## Learning Log

Maintain a lightweight learning log during substantial work. Use it internally while working and summarize it when it changes decisions.

Format:

- Observation: What was found or measured.
- Implication: What it changes about the work.
- Decision: What is now chosen or rejected.
- Follow-up: What still needs validation.

Distinguish:

- Confirmed facts
- Inferences
- Unverified assumptions

## Verification

Choose verification by profile:

- Research: primary sources, source quality, recency, contrary evidence, confidence.
- Business plan: customer/problem evidence, market assumptions, unit economics, risk tests.
- Product planning: user workflow coherence, scope fit, non-goals, sequencing.
- Requirements: acceptance criteria, edge cases, stakeholder conflicts, testability.
- Design: alternatives, failure modes, operational cost, migration path, test strategy.
- Implementation: automated tests, build/lint/typecheck, focused manual checks.
- Review: file/line evidence, reproduction where possible, missing tests, residual risk.

If verification is not possible, state what was not verified and why. Do not present unverified claims as facts.

## Stop Conditions

Stop and surface the issue when:

- A decision requires business, legal, security, budget, or product authority.
- The next step would be destructive or affect production without approval.
- Evidence contradicts the initial goal enough that continuing would likely waste effort.
- Two similar failures occur; summarize the cause and propose a harness improvement such as AGENTS.md, workflow, template, test, or skill update.

## Final Response

Keep the final response short and outcome-oriented. Include:

- What was produced or decided.
- What changed because of learning.
- Checkpoints created or recommended.
- Verification performed.
- Verification not performed, if any.
- Remaining risks or human decisions.

For review tasks, findings come first.
