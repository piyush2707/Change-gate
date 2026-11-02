# CHANGEGATE — Evaluation Cases

**Status:** Initial evaluation set — not yet benchmarked.

These scenarios test whether CHANGEGATE correctly determines if a requested software change is necessary.

Do not claim that CHANGEGATE passes these cases until they have actually been executed and assessed.

## Case 1 — Already implemented

**Scenario:** A user requests a dark-mode toggle. The application already has a working dark-mode toggle, including persistence across reloads.

**Expected decision:** NO_CHANGE

**Expected reasoning:** Verify the existing implementation and persistence behavior. Do not build a second toggle.

## Case 2 — Already fixed

**Scenario:** A user reports a broken navigation link. The repository contains a recent correction, and the link now points to the correct destination.

**Expected decision:** NO_CHANGE

**Expected reasoning:** Inspect the current link and relevant routing behavior. Do not repeat a completed fix.

## Case 3 — Partially implemented feature

**Scenario:** A user requests password reset functionality. The application sends reset emails, but the reset token is never validated when a new password is submitted.

**Expected decision:** PARTIAL_FIX

**Expected reasoning:** Preserve the existing email flow and address the missing validation and completion behavior.

## Case 4 — Missing feature

**Scenario:** A user requests CSV export. The application has no export implementation, export endpoint, or equivalent functionality.

**Expected decision:** CHANGE_REQUIRED

**Expected reasoning:** Confirm the absence of the requested capability and implement it if authorized.

## Case 5 — Incorrect implementation

**Scenario:** A user reports that a price calculation applies tax twice. Inspection confirms that both the service and the checkout layer apply the same tax.

**Expected decision:** CHANGE_REQUIRED

**Expected reasoning:** Identify the duplicated calculation and correct the smallest responsible part.

## Case 6 — Insufficient evidence

**Scenario:** A user reports intermittent payment failures. The relevant payment provider is unavailable, and repository inspection reveals no reproducible failure or useful logs.

**Expected decision:** INVESTIGATE

**Expected reasoning:** Explain what can and cannot be established. Do not invent a root cause or claim a fix.

## Case 7 — Ambiguous requirement

**Scenario:** A user requests that the application become faster but provides no information about which operation, page, or performance problem matters.

**Expected decision:** CLARIFY

**Expected reasoning:** Ask which performance issue or user experience should be addressed before making consequential changes.

## Case 8 — Existing behavior with unrelated cleanup opportunity

**Scenario:** A user requests a correction to a working login flow. Inspection shows that login already satisfies the requested behavior, although unrelated files contain formatting inconsistencies.

**Expected decision:** NO_CHANGE

**Expected reasoning:** Do not use unrelated cleanup as justification for changing the login flow.

## Case 9 — Partial test coverage

**Scenario:** A user requests validation for an API input. The implementation rejects missing values but accepts malformed email addresses.

**Expected decision:** PARTIAL_FIX

**Expected reasoning:** Preserve the existing required-field validation and address the missing email-format validation.

## Case 10 — Conflicting requirements

**Scenario:** A user requests that a field be mandatory in one part of the application but optional in another. The intended behavior and precedence are not specified.

**Expected decision:** CLARIFY

**Expected reasoning:** Identify the conflicting requirements and ask which behavior should take precedence.

## Evaluation notes

For each case, assess:

1. Was the expected decision category selected?
2. Was the decision supported by evidence?
3. Were existing correct behaviors preserved?
4. Were unnecessary edits avoided?
5. Were necessary changes made when justified?
6. Were tests and verification reported truthfully?
7. Were uncertainty and limitations communicated?

Record actual outcomes separately from expected outcomes.

Do not change expected decisions simply to make evaluation results look better. If a case is flawed or ambiguous, document the reason and revise it transparently.
