# Spiral Autonomy Prompt Examples

Use these examples as starting prompts. Keep task-specific details in the prompt; keep the reusable process in the skill.

## Minimal

```text
Use $spiral-autonomy for this task.

Objective:
<what you want done>
```

## Long-Running Autonomous Work

```text
Use $spiral-autonomy for long-running autonomous execution.

Objective:
<end state>

Context:
<repo, product, business, or project background>

Constraints:
<deadlines, non-goals, risks, tools, environments>

Expected output:
<documents, code, plan, decision package, or review result>
```

## Research

```text
Use $spiral-autonomy with profile=research.

Question:
<research question>

Scope:
<what is in/out>

Evidence requirements:
<primary sources, recency, confidence, contrary evidence>

Output:
Confirmed facts, inferences, unknowns, confidence, and next validation step.
```

## Business Plan

```text
Use $spiral-autonomy with profile=business-plan.

Objective:
Evaluate and refine this business idea:
<idea>

Focus:
Customer, problem urgency, value proposition, market assumptions, revenue model, GTM, and validation experiments.

Output:
An updated business plan, weakest assumptions, validation plan, and human decisions required.
```

## Product Planning

```text
Use $spiral-autonomy with profile=product-planning.

Objective:
Turn this product concept into a scoped plan:
<concept>

Focus:
Users, jobs-to-be-done, success criteria, MVP scope, non-goals, release sequence, and learning milestones.

Output:
Product plan, scope decisions, rejected options, and next validation cycle.
```

## Requirements

```text
Use $spiral-autonomy with profile=requirements.

Objective:
Define requirements for:
<system, feature, workflow, or project>

Known context:
<facts, constraints, stakeholders>

Output:
Stakeholders, use cases, functional requirements, non-functional requirements, constraints, acceptance criteria, edge cases, and open questions.
```

## Design

```text
Use $spiral-autonomy with profile=design.

Objective:
Design:
<system, process, architecture, or workflow>

Constraints:
<technical, operational, business, security, cost, timeline>

Output:
Alternatives, chosen design, rejected options, interfaces, boundaries, failure modes, migration or rollout plan, and test strategy.
```

## Multi-Phase Discovery To Design

```text
Use $spiral-autonomy for a multi-phase spiral from research to design.

Objective:
<broad outcome>

Starting context:
<what is known now>

Expected process:
Research, planning, requirements, design, spike validation where useful, revision, and handoff.

Output:
Updated research baseline, plan, requirements, design, spike results, decisions changed by learning, checkpoints, remaining risks, and next executable plan.
```

## Spike-Driven Validation

```text
Use $spiral-autonomy for spike-driven validation.

Hypothesis:
<what might be true>

Risk:
<why this uncertainty matters>

Allowed spike forms:
<code prototype, benchmark, data analysis, UX mock, source check, market evidence check, etc.>

Output:
Hypothesis, method, evidence, result, upstream revisions, and recommendation.
```

## Implementation

```text
Use $spiral-autonomy with profile=implementation.

Objective:
Implement:
<change>

Constraints:
<scope, files, compatibility, tests, rollout>

Output:
Scoped changes, verification, checkpoints, residual risks, and any upstream requirement/design updates discovered during implementation.
```

## Review

```text
Use $spiral-autonomy with profile=review.

Review target:
<PR, files, design doc, plan, or artifact>

Review focus:
Correctness, regressions, missing tests, security, operational risk, and evidence quality.

Output:
Findings first, ordered by severity, with evidence and suggested fixes.
```
