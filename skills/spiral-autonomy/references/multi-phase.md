# Multi-Phase Spiral

Use this reference when one session must cover more than one upstream phase, such as research -> planning -> requirements -> design -> spike -> revision.

## Principles

- Treat every phase output as provisional until later evidence survives review or validation.
- Prefer small experiments over speculative precision.
- Move backward when evidence changes the premise.
- Keep phase artifacts traceable to facts, assumptions, decisions, and open questions.
- Checkpoint after meaningful phase baselines and after evidence changes direction.

## Default Flow

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

Exit when there is enough evidence to frame a provisional plan, not when everything is known.

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

Exit when there is a clear enough direction to define requirements.

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

Exit when requirements are testable enough to evaluate designs.

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

Exit when the largest unresolved risk is identified.

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

Spike rules:

- Define the hypothesis before the spike.
- Define pass/fail or decision criteria before interpreting results.
- Keep the spike isolated unless the user asks to productionize it.
- Prefer deleting or quarantining throwaway code after extracting learning.
- If keeping spike artifacts, label them clearly and do not mix them with production implementation.

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

### 7. Handoff

Goal: leave an executable next step.

Outputs:

- Current decision package
- Updated plan/requirements/design
- Evidence and checkpoints
- Remaining risks
- Next cycle recommendation
- Human decisions required

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
