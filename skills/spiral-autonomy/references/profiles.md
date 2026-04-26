# Spiral Autonomy Profiles

Use this reference when the task profile is unclear or when a profile-specific output shape would improve the result.

## research

Use for investigation, comparison, technical discovery, market facts, legal/regulatory checks, and source-based synthesis.

Outputs:

- Question and scope
- Confirmed facts
- Evidence table with source quality
- Conflicting evidence
- Inferences
- Unknowns
- Confidence level
- Next validation step
- Checkpoint recommendation for durable evidence, if useful

Verification:

- Prefer primary sources.
- Check recency for unstable facts.
- Separate source claims from your conclusions.

## business-plan

Use for new business, strategy, pricing, GTM, financial model, or venture planning.

Outputs:

- Target customer
- Problem and urgency
- Proposed value
- Market and segment assumptions
- Competitive alternatives
- Revenue and cost hypotheses
- Go-to-market motion
- Key risks
- Validation experiments
- Checkpoint recommendation for decisions or evidence

Verification:

- Identify the weakest assumption.
- Prefer tests that reduce market, willingness-to-pay, distribution, or delivery risk.

## product-planning

Use for product concepts, roadmaps, feature prioritization, MVP scope, and discovery.

Outputs:

- Users and jobs-to-be-done
- Success criteria
- Proposed scope
- Non-goals
- User workflows
- Tradeoffs
- Release sequence
- Learning milestones
- Checkpoint recommendation for scope or roadmap changes

Verification:

- Check whether each feature supports a user job or learning objective.
- Avoid roadmap detail beyond the evidence level.

## requirements

Use for requirement definition, acceptance criteria, stakeholder alignment, and scope clarification.

Outputs:

- Stakeholders
- Use cases
- Functional requirements
- Non-functional requirements
- Constraints
- Acceptance criteria
- Edge cases
- Open questions
- Traceability to evidence or decisions
- Checkpoint recommendation for requirement baseline changes

Verification:

- Requirements must be testable or explicitly marked as policy/design constraints.
- Call out conflicts and missing authority.

## design

Use for system design, architecture, process design, organizational design, and technical planning.

Outputs:

- Context and constraints
- Alternatives considered
- Chosen design
- Rejected options and reasons
- Interfaces and boundaries
- Data or process flow
- Operational model
- Failure modes
- Migration or rollout plan
- Test strategy
- Checkpoint recommendation for hard-to-reverse decisions

Verification:

- Stress the design against failure modes, future change, and operational ownership.
- Mark decisions that are hard to reverse.

## implementation

Use for coding or other concrete execution work.

Outputs:

- Scoped plan
- Files or artifacts changed
- Tests added or updated
- Verification results
- Integration notes
- Remaining risks
- Checkpoint commit recommendation when the patch is coherent

Verification:

- Run focused tests first, broader tests when blast radius is larger.
- Keep unrelated refactors separate.
- Preserve user changes.

## review

Use for code review, design review, plan review, or risk review.

Outputs:

- Findings first, ordered by severity
- Evidence with file/line, source, or artifact reference
- Impact
- Suggested fix or decision
- Missing tests
- Residual risk
- Checkpoint recommendation for review evidence or follow-up scope

Verification:

- Prefer reproducible evidence.
- Do not spend most of the answer on summary when findings exist.
