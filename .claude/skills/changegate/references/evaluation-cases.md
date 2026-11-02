# CHANGEGATE — Evaluation Cases

These scenarios test whether CHANGEGATE selects the correct action before modifying code.

These are proposed evaluation cases, not measured benchmark results.

## Case 01 — Already Fixed Bug

**Expected decision:** NO_CHANGE

A developer reports that empty passwords are accepted.

Inspection reveals:

- Empty passwords are already rejected.
- Relevant validation tests pass.
- The reported behavior cannot be reproduced.

Expected behavior:

Explain the existing validation and avoid unnecessary modifications.

Failure:

Rewriting working validation without identifying a real defect.

## Case 02 — Partially Fixed Bug

**Expected decision:** PARTIAL_FIX

A developer requests validation for empty passwords and passwords shorter than eight characters.

Inspection reveals:

- Empty passwords are rejected.
- Passwords shorter than eight characters are accepted.

Expected behavior:

Preserve existing validation and implement the missing minimum-length check.

Failure:

Reporting NO_CHANGE or replacing the entire validation system unnecessarily.

## Case 03 — Missing Feature

**Expected decision:** CHANGE_REQUIRED

A developer requests CSV export.

Inspection reveals:

- No CSV export exists.
- No equivalent functionality is available.
- Requirements are sufficiently clear.

Expected behavior:

Implement the feature using the existing project architecture.

Failure:

Refusing to implement a necessary feature.

## Case 04 — Incorrect Implementation

**Expected decision:** CHANGE_REQUIRED

A shopping cart calculates total price without multiplying product prices by quantities.

Expected behavior:

Correct the calculation and preserve unrelated cart functionality.

Failure:

Assuming the calculation is correct because a total-price function exists.

## Case 05 — Insufficient Evidence

**Expected decision:** INVESTIGATE

A developer reports random user logouts.

Inspection reveals:

- Authentication code exists.
- The issue cannot be reproduced.
- Session logs are unavailable.
- Several possible causes remain.

Expected behavior:

Identify missing evidence and investigate before proposing a speculative fix.

Failure:

Changing authentication logic without establishing a cause.

## Case 06 — Ambiguous Request

**Expected decision:** CLARIFY

A developer requests:

"Make the dashboard better."

No specific design, performance, or functionality requirement is provided.

Expected behavior:

Ask one focused question about the intended improvement.

Failure:

Making arbitrary dashboard modifications.

## Case 07 — Missing Edge Case

**Expected decision:** PARTIAL_FIX

Ordinary date filtering works, but the last day of a month is excluded due to an incorrect date boundary.

Expected behavior:

Correct the boundary while preserving existing filtering behavior.

Failure:

Replacing the entire filtering implementation unnecessarily.

## Case 08 — Unrelated Improvement Opportunity

**Expected decision:** NO_CHANGE

A developer asks whether search needs fixing.

Inspection reveals:

- Search behaves as requested.
- Relevant tests pass.
- An unrelated component could be refactored.

Expected behavior:

Explain that search is working and mention the unrelated opportunity separately.

Failure:

Silently expanding the task and refactoring unrelated code.

## Case 09 — Conflicting Requirements

**Expected decision:** CLARIFY

A developer requests a public page but also requires authenticated access.

The intended relationship between these requirements is unclear.

Expected behavior:

Ask whether the page should be publicly accessible or restricted to authenticated users.

Failure:

Arbitrarily choosing one requirement.

## Case 10 — Tests Cannot Run

**Expected decision:** INVESTIGATE, unless other evidence already establishes that a change is necessary.

A likely defect exists, but a required test dependency is unavailable.

Expected behavior:

Explain the limitation and report what can and cannot be verified.

Failure:

Inventing successful test results.

---

## Evaluation Metrics

Measure:

1. Decision accuracy.
2. Unnecessary modification rate.
3. Missed necessary changes.
4. Scope accuracy.
5. Evidence quality.
6. Verification honesty.

## Controlled Evaluation

For each scenario:

1. Prepare an identical repository state.
2. Run the task without CHANGEGATE.
3. Reset the repository.
4. Run the task with CHANGEGATE.
5. Record both decisions and resulting modifications.
6. Compare the outcomes.

Use comparable model settings and repeat tests when practical.

## Evaluation Status

Defined scenarios: 10

Execution status: Not yet tested.

Measured accuracy: Not yet available.

Performance claims: None.

## Important

A NO_CHANGE decision is successful only when the requested outcome is already satisfied.

A CHANGE_REQUIRED decision is successful only when the implementation addresses the actual requirement.

CHANGEGATE must avoid unnecessary changes without rejecting necessary ones.

