# Multi-Phase Spiral

Use this reference when one session must cover more than one upstream phase, such as research -> planning -> requirements -> design -> spike -> revision. Multi-phase work is a mission loop, not a checklist to complete once.

## Principles

- Treat every phase output as provisional until later evidence survives review or validation.
- Prefer small experiments over speculative precision.
- Move backward when evidence changes the premise.
- Keep phase artifacts traceable to facts, assumptions, decisions, and open questions.
- Checkpoint after meaningful phase baselines, validation artifacts, revisions, review boundaries, and evidence changes in direction.
- Continue while local, non-destructive work can materially improve the objective.
- Do not use handoff as the first exit when validation or revision can still be done locally.

## Mission Loop

Run the phases below as a loop. After each artifact, update the uncertainty frontier and choose the next executable action. Re-enter earlier phases whenever evidence changes the plan, requirements, or design.

Before stopping, verify that the objective is achieved or that the next necessary step truly requires external authority, unavailable data, destructive action, or production impact.

When the active checkpoint policy is `auto-commit with limits`, create frequent small commits as phase artifacts land. Do not wait until the full mission or full phase sequence is complete.

### 1. Research Baseline

Goal: establish the factual and uncertainty map.

Outputs:

- Core question
- Confirmed facts
- Constraints
- Unknowns
- Competing interpretations
- Highest-risk assumptions
- Evidence quality

Move forward when there is enough evidence to frame a provisional plan, not when everything is known. Keep unresolved high-risk assumptions in the action queue.

### 2. Planning Baseline

Goal: turn facts into a provisional direction.

Use `business-plan` when the question is commercial or organizational. Use `product-planning` when the question is product scope, user value, or roadmap.

Outputs:

- Target customer/user
- Problem or job
- Value hypothesis
- Scope and non-goals
- Success criteria
- Strategy or release sequence
- Assumptions that must be tested

Move forward when there is a clear enough direction to define requirements. Keep value, GTM, economics, and channel assumptions queued for validation.

### 3. Requirements Baseline

Goal: convert direction into testable needs.

Outputs:

- Stakeholders
- Use cases
- Functional requirements
- Non-functional requirements
- Constraints
- Acceptance criteria
- Edge cases
- Open questions

Move forward when requirements are testable enough to evaluate designs. Keep weak or untestable requirements queued for revision.

### 4. Design Baseline

Goal: choose an approach and expose risk.

Outputs:

- Alternatives considered
- Chosen design
- Rejected options
- Interfaces and boundaries
- Data/process flow
- Operational model
- Failure modes
- Test strategy
- Hard-to-reverse decisions

Move forward when the largest unresolved risk is identified. The next action should usually validate that risk.

### 5. Spike Validation

Goal: reduce the highest-risk uncertainty with the smallest practical experiment.

Spike forms:

- Code prototype
- Throwaway technical integration
- Benchmark or load test
- API/source documentation check
- Data sample analysis
- UX workflow sketch or clickable mock
- Pricing/unit economics model
- Market/channel evidence check
- Policy/legal feasibility check
- Fixture or sample output
- Schema draft
- Competitive matrix
- Worked example
- Interview script with scoring rubric
- Risk test

Spike rules:

- Define the hypothesis before the spike.
- Define pass/fail or decision criteria before interpreting results.
- Keep the spike isolated unless the user asks to productionize it.
- Prefer deleting or quarantining throwaway code after extracting learning.
- If keeping spike artifacts, label them clearly and do not mix them with production implementation.
- For mission-mode multi-phase work, create at least one concrete validation artifact before handoff unless blocked by a real stop condition.

Spike output:

- Hypothesis
- Method
- Evidence
- Result
- Decision impact
- What to revise upstream
- Follow-up risk

### 6. Revision Pass

Goal: reconcile later evidence with earlier artifacts.

Update:

- Research conclusions if facts changed.
- Plan if value, customer, scope, or strategy changed.
- Requirements if acceptance criteria, constraints, or edge cases changed.
- Design if interfaces, boundaries, data model, or operations changed.
- Verification plan if the real risk moved.

Explicitly list:

- Kept assumptions
- Changed assumptions
- Rejected assumptions
- New open questions

### 7. Review And Continue Gate

Goal: decide whether the mission should continue locally.

Check:

- Whether the objective is achieved against the definition of done.
- Whether a local, non-destructive next action can improve evidence, design maturity, business viability, implementation quality, or verification.
- Whether that action can produce a durable artifact or upstream revision.
- Whether any stop condition is real rather than a generic future need for human judgment.

If useful local work remains, continue the loop instead of handing off.

### 8. Handoff

Goal: leave an executable next step only when the mission is complete enough for the current authority or when a real stop condition blocks further local progress.

Outputs:

- Current decision package
- Updated plan/requirements/design
- Evidence and checkpoints
- Remaining risks
- Next cycle recommendation
- Human decisions required
- Why stopping is valid under mission mode

## Profile Switching

Switch profiles based on the work now needed:

- Need facts or source confidence -> `research`
- Need value, market, customer, GTM, economics -> `business-plan`
- Need product direction or scope -> `product-planning`
- Need testable needs -> `requirements`
- Need architecture/process choice -> `design`
- Need experiment or prototype -> `implementation` plus spike rules
- Need critique before proceeding -> `review`

Do not ask the user to choose a profile when the next profile is inferable from evidence.
