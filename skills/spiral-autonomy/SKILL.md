---
name: spiral-autonomy
description: Use when Codex should run a learning-driven spiral process for ambiguous or evolving work across research, business planning, product planning, requirements, design, implementation, testing, or review. Triggers include requests for autonomous execution, high-agency planning, iterative discovery, hypothesis-driven work, upstream revision after implementation findings, subagent coordination, or maximizing learning from investigation/prototyping.
license: MIT
---

# Spiral Autonomy

## Operating Model

Run the task as a spiral process: treat the initial request as a provisional hypothesis, increase resolution through investigation or execution, and revise upstream assumptions when evidence changes.

Default to mission-driven autonomy. When this skill is selected, the primary job is to keep working toward the user's objective until the objective is achieved or a real stop condition is reached. Do not treat a first analysis pass, planning document, handoff, or next-steps list as completion when useful local work remains.

Shorten the work only when the user explicitly narrows the request, for example "light pass", "one cycle", "plan only", "research only", "do not implement", or a similarly clear limit. Otherwise, ambiguous or high-level goals should be decomposed into an executable queue and advanced autonomously.

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

## Default Mission Mode

Use mission mode by default:

- Make objective completion the governing criterion, not cycle count.
- Maintain the current uncertainty frontier: the assumptions, missing evidence, weak designs, untested workflows, or quality risks that most threaten the objective.
- Maintain an executable action queue. When an action completes, add the next useful local action if it can improve the result.
- Prefer durable artifacts over discussion-only progress: source notes, models, schemas, examples, prototypes, tests, reviews, decision records, or upstream revisions.
- When delegation is available, use the maximum useful parallelism allowed by the active environment and task constraints. Keep subagents busy with concrete high-load research, design, implementation, testing, and review work until the objective is achieved or a real stop condition is reached.
- Before handing off, perform the strongest practical validation available within local authority.
- Treat handoff as an artifact for real external dependency or human authority, not the default exit.

For broad goals such as maturing a business plan, reaching a market-winning design, autonomous development, end-to-end discovery, or high-agency planning, continue through research, artifact creation, validation, critique, and revision until local non-destructive work is exhausted.

## Start

Begin by stating the user's objective and the first move in one or two sentences.

Then build a compact working frame:

- Mission objective
- Definition of done
- Known facts
- Assumptions
- Open questions
- Current profile
- Phase sequence, if multi-phase
- Current uncertainty frontier
- Executable action queue
- Evidence threshold
- Stop only when
- Checkpoint policy

If working in a repository, inspect local operating assets first: `AGENTS.md`, `.codex/`, README, CI/workflows, package manifests, task runners, and relevant docs. Prefer repo instructions over generic defaults.

## Delegation

Default to delegation when subagents are available and allowed by the active environment. Do not wait for the user to separately request parallelism when this skill is already being used for autonomous work.

Mission mode does not depend on subagents. If delegation is unavailable or blocked by higher-priority system rules, continue autonomously as a single agent using the same executable queue.

When delegating:

- Keep the critical path local.
- Maximize useful parallelism without creating duplicate work or write conflicts.
- Delegate bounded high-load work that can run in parallel.
- Assign each subagent a concrete output, not a search task: research evidence, design options, implementation patches, test execution and analysis, review findings, risk analysis, or validation artifacts.
- Give each implementation subagent an explicit write scope.
- Tell workers they are not alone in the codebase and must not revert others' changes.
- Separate implementation and review when practical.
- Do not use subagents as generic search engines.
- Keep subagents continuously supplied from the executable action queue. When a subagent completes, integrate the result, update the uncertainty frontier, and immediately assign the next bounded concrete task if one remains.

Good delegated outputs include: evidence table, design option with tradeoffs, scoped patch, test result analysis, risk review, acceptance criteria critique, or market hypothesis critique.

## Spiral Cycle

Run mission loops until the objective is achieved or a real stop condition is reached. Keep each loop small enough that learning can change direction before large sunk cost accumulates, but do not stop merely because one coherent loop completed.

Each loop:

1. State the hypothesis or question.
2. Gather only the context needed for the next decision.
3. Produce a small artifact: analysis, design, prototype, patch, test, review, or decision record.
4. Verify using the strongest practical method for the profile.
5. Extract learning.
6. Update upstream artifacts: objective, requirements, design, plan, acceptance criteria, or task split.
7. Update the executable action queue and uncertainty frontier.
8. Decide whether to place a checkpoint.
9. Apply the continue gate before any final response.

Prefer evidence over momentum. If implementation reveals the premise is wrong, revise requirements or design before continuing implementation.

## Continue Gate

Before final response, check:

- Is the mission objective achieved according to the definition of done?
- Is there a useful local, non-destructive next action available without human authority?
- Would that action reduce a major uncertainty, improve design maturity, improve business viability, improve implementation quality, or strengthen verification?
- Can it produce or update a durable artifact such as a source note, schema, model, fixture, sample output, spike, test, critique, decision record, or upstream revision?

If the objective is not achieved and the remaining action answers yes to the last three questions, continue instead of finalizing. Ask for human judgment only when the next necessary step truly requires external authority, unavailable data, destructive action, production impact, or a business/legal/security/product decision.

## Multi-Phase Work

When the user's goal spans multiple upstream phases, do not force a linear waterfall. Treat each phase output as a provisional artifact that can be revised by later evidence.

Default mission loop:

1. Research: establish facts, constraints, and uncertainty.
2. Product or business planning: frame value, users/customers, scope, and strategy.
3. Requirements: define testable needs, constraints, and acceptance criteria.
4. Design: evaluate alternatives and choose a coherent approach.
5. Spike validation: run the smallest practical experiment, prototype, code spike, benchmark, model, or source check that can reduce the highest-risk uncertainty.
6. Revision: update research conclusions, plan, requirements, and design based on spike evidence.
7. Review: critique the result against the mission objective and evidence threshold.
8. Continue or handoff: continue when local work remains; hand off only when a real stop condition is reached.

Move backward whenever later evidence invalidates earlier assumptions. Record what changed and why. Do not preserve an earlier plan merely for consistency.

Use spikes for high-risk assumptions, unclear feasibility, unknown integration behavior, UX/workflow ambiguity, performance uncertainty, data availability, cost assumptions, market/channel assumptions, or requirements that are difficult to make testable.

For multi-phase mission work, create at least one concrete validation artifact before handoff unless blocked by a real stop condition. Examples include a fixture or sample output, schema draft, pricing model, competitive matrix, worked example, prototype, benchmark, interview script with scoring rubric, or risk test. After creating the validation artifact, revise upstream artifacts based on what it showed.

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

- The next necessary decision requires business, legal, security, budget, or product authority, and no useful validation preparation remains.
- The next step would be destructive or affect production without approval.
- Evidence contradicts the initial goal enough that continuing would likely waste effort.
- Two similar failures occur; summarize the cause and propose a harness improvement such as AGENTS.md, workflow, template, test, or skill update.

Do not stop only because a human will eventually make a decision. First complete any local preparation that can improve that decision, such as hypothesis comparison, numeric modeling, evidence collection, validation design, questionnaire creation, fixture/schema/example creation, or risk review.

## Final Response

Keep the final response short and outcome-oriented. Include:

- What was produced or decided.
- What changed because of learning.
- Checkpoints created or recommended.
- Verification performed.
- Verification not performed, if any.
- Remaining risks or human decisions.
- Why stopping is valid under mission mode.

For review tasks, findings come first.
