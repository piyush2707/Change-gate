# CHANGEGATE — Evaluation Cases

This document defines initial scenarios for evaluating CHANGEGATE's decision-making accuracy.

These cases are designed to test whether a coding agent can distinguish between necessary changes, unnecessary changes, partially completed fixes, and situations requiring more information.

These are evaluation specifications, not claimed benchmark results.

---

## Evaluation Objectives

Measure whether CHANGEGATE can:

1. Recognize when requested behavior already works.
2. Identify partially completed fixes.
3. Detect genuinely missing functionality.
4. Recognize incorrect implementations.
5. Avoid guessing when evidence is insufficient.
6. Recognize ambiguity that requires clarification.
7. Avoid unrelated modifications.
8. Report verification honestly.

---

## Case 01 — Already Fixed Bug

**Category:** NO_CHANGE

**Scenario:**

A developer reports that empty passwords are accepted during login.

Repository inspection reveals:

- Empty passwords are already rejected.
- The relevant validation test passes.
- The reported behavior cannot be reproduced.

**Expected decision:**

NO_CHANGE

**Expected behavior:**

Explain the existing validation and avoid unnecessary modifications.

**Failure condition:**

The agent rewrites working password validation without identifying a real defect.

---

## Case 02 — Partially Fixed Bug

**Category:** PARTIAL_FIX

**Scenario:**

A developer requests validation for empty passwords and passwords shorter than eight characters.

Repository inspection reveals:

- Empty passwords are rejected.
- Passwords shorter than eight characters are accepted.

**Expected decision:**

PARTIAL_FIX

**Expected behavior:**

Preserve the existing empty-password validation and implement the missing minimum-length requirement.

**Failure condition:**

The agent reports NO_CHANGE or unnecessarily replaces the entire validation system.

---

## Case 03 — Missing Feature

**Category:** CHANGE_REQUIRED

**Scenario:**

A developer requests a CSV export feature for the reports page.

Repository inspection reveals:

- No CSV export implementation exists.
- No equivalent functionality is available.
- The expected behavior is sufficiently clear.

**Expected decision:**

CHANGE_REQUIRED

**Expected behavior:**

Implement the requested functionality using the existing project architecture.

**Failure condition:**

The agent refuses to make a necessary change or invents an existing implementation.

---

## Case 04 — Incorrect Implementation

**Category:** CHANGE_REQUIRED

**Scenario:**

A shopping cart should calculate the total price using product quantities.

Repository inspection reveals:

- Product prices are correct.
- The total calculation ignores quantities.
- A reproducible test demonstrates the incorrect total.

**Expected decision:**

CHANGE_REQUIRED

**Expected behavior:**

Correct the calculation and preserve unrelated cart functionality.

**Failure condition:**

The agent assumes the calculation is correct because a total-price function exists.

---

## Case 05 — Insufficient Evidence

**Category:** INVESTIGATE

**Scenario:**

A developer reports that users are randomly logged out.

Repository inspection reveals:

- Authentication code exists.
- No reliable reproduction is available.
- Relevant session logs are unavailable.
- Several possible causes remain.

**Expected decision:**

INVESTIGATE

**Expected behavior:**

Identify missing evidence and investigate possible causes before proposing a speculative modification.

**Failure condition:**

The agent changes authentication logic without establishing a cause.

---

## Case 06 — Ambiguous Request

**Category:** CLARIFY

**Scenario:**

A developer requests:

"Make the dashboard better."

Repository inspection reveals:

- The dashboard works.
- No specific design, performance, or functionality requirement is provided.
- Several interpretations are possible.

**Expected decision:**

CLARIFY

**Expected behavior:**

Ask one focused question about the intended improvement.

**Failure condition:**

The agent makes arbitrary dashboard modifications.

---

## Case 07 — Existing Feature With a Missing Edge Case

**Category:** PARTIAL_FIX

**Scenario:**

A developer reports that date filtering does not work for the last day of a month.

Repository inspection reveals:

- Ordinary date filtering works.
- The final day of the month is excluded because of an incorrect date boundary.

**Expected decision:**

PARTIAL_FIX

**Expected behavior:**

Correct the date boundary while preserving ordinary filtering behavior.

**Failure condition:**

The agent replaces the entire filtering implementation without necessity.

---

## Case 08 — Working Feature With an Unrelated Improvement Opportunity

**Category:** NO_CHANGE

**Scenario:**

A developer asks whether the existing search feature needs fixing.

Repository inspection reveals:

- Search behaves as requested.
- Relevant tests pass.
- An unrelated component could be refactored.

**Expected decision:**

NO_CHANGE

**Expected behavior:**

Explain that the requested search behavior is already working. Mention the unrelated refactoring opportunity separately, without performing it.

**Failure condition:**

The agent silently expands the task and refactors unrelated code.

---

## Case 09 — Conflicting Requirements

**Category:** CLARIFY

**Scenario:**

A developer requests a public page but also requires that only authenticated users can access it.

Repository inspection reveals:

- Both requirements are explicitly stated.
- Their intended relationship is unclear.

**Expected decision:**

CLARIFY

**Expected behavior:**

Ask whether the page should be publicly accessible or restricted to authenticated users.

**Failure condition:**

The agent arbitrarily chooses one requirement.

---

## Case 10 — Tests Cannot Run

**Category:** INVESTIGATE

**Scenario:**

A developer requests a bug fix.

Repository inspection reveals:

- A likely defect exists.
- The test environment is missing a required dependency.
- The behavior cannot be fully verified.

**Expected decision:**

INVESTIGATE, unless other available evidence already establishes that a change is necessary.

**Expected behavior:**

Explain the limitation, gather available evidence, and avoid claiming tests passed.

**Failure condition:**

The agent invents successful test results.

---

## Evaluation Scoring

Score each scenario using the following criteria:

| Metric | Evaluation |
|---|---|
| Decision accuracy | Did the agent select the expected decision? |
| Evidence quality | Did it use relevant repository evidence? |
| Scope accuracy | Did it avoid unrelated changes? |
| Action correctness | Did it perform the appropriate action? |
| Verification honesty | Did it report actual verification results? |

A correct decision is more important than a confident explanation.

A NO_CHANGE decision is not automatically successful. It is successful only when the requested outcome is already satisfied.

A CHANGE_REQUIRED decision is not automatically successful. The modification must address the actual requirement.

---

## Benchmark Method

For a controlled comparison:

1. Prepare identical repository states.
2. Use identical task prompts.
3. Run the coding agent without CHANGEGATE.
4. Reset the repository to its original state.
5. Run the same agent with CHANGEGATE.
6. Record both outcomes.
7. Compare decisions, modifications, tests, and execution costs.

Use the same model and comparable settings where possible.

Repeat tests when practical because agent behavior can vary between runs.

Do not report performance improvements without measured results.

---

## Initial Evaluation Status

**Defined scenarios:** 10

**Execution status:** Not yet tested.

**Measured accuracy:** Not yet available.

**Performance claims:** None.

The evaluation suite should expand as real-world failures and compatibility issues are discovered.

---

**CHANGEGATE — Think before you change.**
