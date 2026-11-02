
# CHANGEGATE — Decision Rules

This document defines the decision rules used by CHANGEGATE when evaluating software change requests.

The objective is to select the correct action based on repository evidence.

The goal is not to avoid code changes.

The goal is to avoid unnecessary changes while ensuring necessary changes are not rejected.

---

## 1. Decision Priority

Use this order:

1. Understand the requested outcome.
2. Identify the relevant requirements.
3. Inspect the current implementation.
4. Gather supporting evidence.
5. Identify uncertainty.
6. Select one primary decision.
7. Explain the reasoning.
8. Act according to the decision.
9. Verify the result when applicable.

Do not skip inspection merely because a proposed solution seems obvious.

---

## 2. NO_CHANGE

### Definition

Use NO_CHANGE when the requested outcome is already achieved and available evidence supports that conclusion.

### Required evidence

Look for:

- Relevant implementation.
- Existing behavior.
- Applicable tests.
- Relevant configuration.
- Other evidence needed to establish correctness.

### Example

User request:

"Fix the password validation bug."

Inspection finds:

- Password validation is implemented.
- The reported input is handled correctly.
- Relevant tests pass.
- No reproducible defect is found.

Expected decision:

NO_CHANGE

### Required action

- Do not modify code unnecessarily.
- Explain what was inspected.
- Explain why the requested behavior already exists.
- Identify any limitations in the evidence.

### Important distinction

A passing test alone does not prove that every possible case works.

Do not claim complete correctness beyond the evidence available.

---

## 3. PARTIAL_FIX

### Definition

Use PARTIAL_FIX when some requested behavior already works but one or more required conditions remain incomplete or incorrect.

### Required evidence

Identify:

- Which requirements are already satisfied.
- Which requirements remain unsatisfied.
- The specific implementation responsible.
- The smallest appropriate correction.

### Example

User request:

"Make login validation reject empty passwords and passwords shorter than eight characters."

Inspection finds:

- Empty passwords are rejected.
- Passwords shorter than eight characters are accepted.

Expected decision:

PARTIAL_FIX

### Required action

- Preserve the working empty-password validation.
- Implement the missing minimum-length validation.
- Avoid replacing unrelated login functionality.
- Verify both conditions when possible.

### Critical safeguard

Never classify a partially completed fix as NO_CHANGE simply because some of the requested behavior already works.

---

## 4. CHANGE_REQUIRED

### Definition

Use CHANGE_REQUIRED when the requested behavior is missing or the existing implementation demonstrably fails a requirement.

### Required evidence

Establish:

- The expected behavior.
- The actual behavior.
- The relevant implementation or missing functionality.
- Why a modification is necessary.

### Example

User request:

"Add an export button that downloads a CSV report."

Inspection finds:

- No export functionality exists.
- No equivalent feature is available.
- The requirement is sufficiently clear.

Expected decision:

CHANGE_REQUIRED

### Required action

- Implement the smallest suitable solution.
- Respect the existing architecture.
- Avoid unrelated refactoring.
- Run relevant tests when available.
- Inspect the resulting changes.

---

## 5. INVESTIGATE

### Definition

Use INVESTIGATE when the available evidence is insufficient to select a reliable implementation decision.

### Common reasons

- The relevant behavior cannot be reproduced.
- Important files are unavailable.
- Dependencies are missing.
- Tests cannot run.
- The reported issue depends on an unknown environment.
- Existing implementation behavior is unclear.

### Example

User request:

"The application randomly logs users out."

Inspection finds:

- Authentication code is available.
- No reliable reproduction is possible.
- Session expiration settings are unclear.
- Relevant runtime logs are unavailable.

Expected decision:

INVESTIGATE

### Required action

- Gather additional relevant evidence.
- Identify the missing information.
- Avoid speculative fixes.
- Explain what is needed to proceed.

### Important distinction

INVESTIGATE is not a permanent refusal to make changes.

Continue toward a reliable decision when additional evidence becomes available.

---

## 6. CLARIFY

### Definition

Use CLARIFY when ambiguity in the user's request materially affects the correct implementation.

### Common reasons

- Conflicting requirements.
- Multiple plausible interpretations.
- Missing acceptance criteria.
- Unclear expected behavior.
- An implementation choice that requires user preference.

### Example

User request:

"Make the dashboard faster."

Inspection finds:

- Several possible performance bottlenecks.
- No target metric.
- No indication of which user experience matters most.

Expected decision:

CLARIFY, or INVESTIGATE if measurable performance evidence can first narrow the problem.

### Required action

Ask one focused question that resolves the most important ambiguity.

Do not ask unnecessary questions when the answer can be established through repository inspection.

---

## 7. Evidence Quality

Classify evidence according to its strength.

### Strong evidence

Examples:

- Reproducible behavior.
- Relevant passing or failing tests.
- Direct inspection of the implementation.
- Measured runtime results.
- Verified application output.

### Supporting evidence

Examples:

- Related documentation.
- Configuration values.
- Existing code comments.
- Relevant project history.
- Similar implementations elsewhere in the repository.

### Insufficient evidence

Examples:

- Assumptions about how code works.
- Unverified claims.
- Guesswork based on filenames.
- Tests that were not executed.
- Conclusions based only on the existence of a function.

Do not present supporting or insufficient evidence as definitive proof.

---

## 8. Scope Control

Every proposed modification must be connected to a requirement.

Before editing, ask:

- Is this modification necessary for the requested outcome?
- Does it preserve existing behavior?
- Is there a smaller suitable change?
- Does it introduce unrelated refactoring?
- Are there additional risks?

If an unrelated improvement is discovered, report it separately rather than silently expanding the task.

---

## 9. Verification Rules

After modifying code:

1. Inspect the resulting diff.
2. Run relevant tests when available.
3. Check the requested behavior.
4. Identify regressions or unexpected changes.
5. Report what was actually verified.

If a test cannot be run, state that explicitly.

Never invent test results.

Never claim that an implementation is fully verified when only part of it was tested.

---

## 10. Decision Consistency

Use the same decision definitions across supported coding agents.

The exact tools and inspection capabilities may differ between environments.

Do not assume that every agent can access the same tests, logs, history, or runtime.

When evidence is unavailable, report the limitation rather than pretending it exists.

---

## Final Rule

CHANGEGATE must never optimize for fewer edits at the expense of correctness.

A necessary change must not be rejected merely to avoid modifying code.

An unnecessary change must not be made merely because an implementation opportunity exists.

**Choose the action that best satisfies the user's actual requested outcome.**
