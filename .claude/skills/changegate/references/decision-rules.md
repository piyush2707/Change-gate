
# CHANGEGATE — Decision Rules

## Purpose

Determine whether a requested software change is necessary using repository evidence.

The goal is not to minimize edits at all costs. The goal is to make the smallest correct change while preserving working behavior.

## 1. Decision workflow

Follow this sequence:

1. Understand the requested outcome.
2. Identify the relevant requirements.
3. Inspect the existing implementation.
4. Examine available tests and evidence.
5. Compare actual behavior with expected behavior.
6. Identify uncertainty or ambiguity.
7. Select one primary decision.
8. Explain the decision.
9. Act when appropriate and authorized.
10. Verify actual results.

Never skip inspection simply because a solution seems obvious.

## 2. The five decisions

### NO_CHANGE

Use when the requested outcome already works and available evidence supports that conclusion.

Requirements:
- Inspect relevant implementation and behavior.
- Examine applicable tests or other evidence.
- Explain why the requested outcome is already satisfied.
- Report limitations in verification.

Do not modify code merely to demonstrate activity.

A passing test alone does not prove every possible case works.

### PARTIAL_FIX

Use when some requested behavior works but one or more requirements remain incomplete or incorrect.

Requirements:
- Identify what already works.
- Identify what remains incomplete.
- Locate the relevant implementation.
- Make the smallest appropriate correction.
- Preserve working behavior.

Never classify a partially completed fix as NO_CHANGE merely because part of it works.

### CHANGE_REQUIRED

Use when the requested behavior is missing or the existing implementation demonstrably fails a requirement.

Requirements:
- Establish expected behavior.
- Identify actual behavior.
- Explain why a modification is necessary.
- Implement the smallest suitable change when authorized.
- Verify the result using available checks.

Avoid unrelated refactoring.

### INVESTIGATE

Use when available evidence is insufficient for a reliable decision.

Examples:
- The reported behavior cannot be reproduced.
- Important files or dependencies are unavailable.
- Runtime logs are missing.
- An external service cannot be inspected.
- Multiple possible causes remain.

Requirements:
- State what was inspected.
- Identify missing evidence.
- Perform safe, relevant investigation where possible.
- Avoid speculative fixes.
- Explain what is needed to proceed.

INVESTIGATE is not a permanent refusal to make changes. Continue when useful evidence becomes available.

### CLARIFY

Use when ambiguity materially affects the correct implementation.

Examples:
- Conflicting requirements.
- Multiple plausible interpretations.
- Missing acceptance criteria.
- Unclear expected behavior.
- A consequential choice requiring user preference.

Requirements:
- Identify the ambiguity.
- Explain why it matters.
- Ask one focused question.
- Do not silently choose a consequential interpretation.

Do not ask questions that repository inspection can resolve.

## 3. Evidence standards

Prefer direct evidence over assumptions.

Strong evidence:
- Reproduced behavior.
- Relevant tests actually executed.
- Direct inspection of implementation.
- Measured runtime results.
- Verified application output.

Supporting evidence:
- Documentation.
- Configuration.
- Project history.
- Relevant code comments.
- Similar implementations.

Insufficient evidence:
- Guesswork.
- Unverified claims.
- Assumptions based on filenames.
- Tests that were never executed.
- Conclusions based only on the existence of a function.

Documentation and comments may be outdated. Verify important claims against implementation when possible.

Never present weak evidence as definitive proof.

## 4. Partial-fix discipline

For partially implemented behavior, determine:

- Which requirements are satisfied?
- Which requirements remain unsatisfied?
- Is the remaining gap relevant to the request?
- Can the gap be fixed without replacing working behavior?

Preserve completed work and address only the remaining gap.

## 5. Scope control

Before editing, ask:

- Is this change necessary for the requested outcome?
- Does it preserve existing behavior?
- Is there a smaller suitable change?
- Does it introduce unrelated refactoring?
- Does it add unnecessary dependencies?
- Does it change public interfaces without need?

Report unrelated improvement opportunities separately.

## 6. Verification

After modifying code:

1. Inspect the resulting diff.
2. Run relevant tests or checks when available.
3. Check the requested behavior.
4. Look for unintended changes.
5. Report what was actually verified.

If a test cannot run, state that explicitly.

Never invent test results or claim complete verification when only part of the behavior was tested.

## 7. Final decision report

Report:

- **Decision:** one of the five categories.
- **Evidence:** what was actually inspected or tested.
- **Finding:** what already works and what does not.
- **Action:** what was changed, or why no change was made.
- **Verification:** checks performed and actual results.
- **Limitations:** anything important that remains unverified.

## Final rule

CHANGEGATE must never optimize for fewer edits at the expense of correctness.

A necessary change must not be rejected merely to avoid modifying code.

An unnecessary change must not be made merely because an implementation opportunity exists.

**Choose the action that best satisfies the user's actual requested outcome.**
