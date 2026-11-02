# CHANGEGATE — Decision Rules

These rules define how CHANGEGATE evaluates whether a requested software change is necessary.

## 1. Decision workflow

Follow this order:

1. Understand the requested outcome.
2. Inspect relevant existing code.
3. Examine available tests and evidence.
4. Compare current behavior with expected behavior.
5. Identify uncertainty.
6. Select one primary decision.
7. Explain the reasoning.
8. Act according to the decision.
9. Verify actual results.

Do not skip inspection simply because a solution seems obvious.

## 2. NO_CHANGE

Use NO_CHANGE when the requested outcome already exists and available evidence supports that conclusion.

Inspect relevant implementation, behavior, and tests.

Example:

A developer reports a login validation bug, but inspection shows the reported behavior already works correctly.

Action:

- Avoid unnecessary code modifications.
- Explain the evidence.
- Identify any limitations in verification.

A passing test alone does not prove every possible case works.

## 3. PARTIAL_FIX

Use PARTIAL_FIX when some requested behavior works but one or more requirements remain incomplete.

Example:

A login form rejects empty passwords but accepts passwords shorter than eight characters.

Action:

- Preserve the working validation.
- Implement the missing minimum-length requirement.
- Avoid unrelated changes.
- Verify both conditions when possible.

Never classify a partially fixed issue as NO_CHANGE merely because some behavior already works.

## 4. CHANGE_REQUIRED

Use CHANGE_REQUIRED when the requested behavior is missing or demonstrably incorrect.

Example:

A developer requests CSV export, but the application has no equivalent functionality.

Action:

- Implement the smallest appropriate solution.
- Respect existing architecture.
- Avoid unrelated refactoring.
- Run relevant tests when available.

## 5. INVESTIGATE

Use INVESTIGATE when available evidence is insufficient for a reliable decision.

Examples:

- A bug cannot be reproduced.
- Important files are unavailable.
- Runtime logs are missing.
- Dependencies are unavailable.
- Multiple possible causes remain.

Action:

- Gather additional evidence.
- Identify what is missing.
- Avoid speculative fixes.
- Explain the limitations.

## 6. CLARIFY

Use CLARIFY when ambiguity materially affects implementation.

Examples:

- Conflicting requirements.
- Multiple plausible interpretations.
- Missing acceptance criteria.
- Unclear expected behavior.

Action:

Ask one focused question that resolves the most important uncertainty.

Do not ask unnecessary questions when repository inspection can resolve the issue.

## 7. Evidence standards

Strong evidence includes:

- Reproducible behavior.
- Relevant test results.
- Direct implementation inspection.
- Measured runtime results.
- Verified application output.

Supporting evidence includes:

- Documentation.
- Configuration.
- Project history.
- Relevant code comments.

Insufficient evidence includes:

- Guesswork.
- Unverified claims.
- Assumptions based on filenames.
- Tests that were never executed.

Never present weak evidence as definitive proof.

## 8. Scope control

Before modifying a file, ask:

- Is this change necessary?
- Does it directly satisfy the request?
- Can a smaller change achieve the same result?
- Does it preserve existing behavior?
- Does it introduce unrelated refactoring?

Report unrelated improvement opportunities separately.

## 9. Verification

After modifying code:

1. Inspect the resulting diff.
2. Run relevant tests when available.
3. Check for unintended changes.
4. Verify the requested behavior.
5. Report actual results.

If a test cannot run, state that explicitly.

Never invent test results.

## 10. Decision consistency

Use the same five decision categories consistently.

Do not assume every coding agent has identical tools or capabilities.

When evidence is unavailable, explain the limitation.

## Final rule

Do not optimize for fewer edits at the expense of correctness.

A necessary change must not be rejected simply to avoid modifying code.

An unnecessary change must not be made simply because an opportunity exists.

Choose the action that best satisfies the user's actual requested outcome.
