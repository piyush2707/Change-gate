---
name: changegate
description: Evaluate whether a requested software change is necessary before modifying code. Distinguish already-correct, partially fixed, broken, missing, and unclear behavior. Use for bug reports, feature requests, code improvements, and refactoring requests.
---

# CHANGEGATE

Think before you change.

Determine whether a requested software change is necessary before implementing it.

Do not assume every request requires code modifications.

## 1. Understand

Identify:

- The requested outcome.
- The expected behavior.
- The current behavior.
- Relevant requirements and acceptance criteria.

## 2. Inspect

Before editing:

- Read relevant implementation files.
- Inspect related functions and components.
- Examine existing tests.
- Check relevant configuration and documentation.
- Search for existing implementations.
- Inspect project history when useful.

Do not assume code exists merely because a filename suggests it does.

## 3. Evaluate

Compare actual behavior with the requested outcome.

Determine whether the behavior is:

- Already correct.
- Partially implemented.
- Incorrect.
- Missing.
- Impossible to determine with available evidence.
- Ambiguous and requiring clarification.

## 4. Classify

Select exactly one primary decision:

**NO_CHANGE**

The requested outcome already exists and available evidence supports that conclusion.

**PARTIAL_FIX**

Some requested behavior works, but identifiable requirements remain incomplete.

**CHANGE_REQUIRED**

The requested behavior is absent or demonstrably incorrect.

**INVESTIGATE**

More evidence is needed before making a reliable decision.

**CLARIFY**

The request contains ambiguity that materially affects implementation.

## 5. Explain

Report the selected decision and supporting evidence before implementation.

## 6. Act

- NO_CHANGE: Stop without unnecessary edits.
- PARTIAL_FIX: Complete only the missing behavior.
- CHANGE_REQUIRED: Implement the smallest suitable change.
- INVESTIGATE: Gather more evidence.
- CLARIFY: Ask one focused question.

Respect user instructions and environment permissions.

## 7. Verify

When changes are made:

- Inspect the diff.
- Run relevant tests when available.
- Check for unintended modifications.
- Report actual verification results.

Never claim tests passed unless they were actually run.

## Reference documents

The following reference files should be installed alongside this SKILL.md:

- `references/decision-rules.md`
- `references/evaluation-cases.md`

Read `references/decision-rules.md` before classifying a request.

Read `references/evaluation-cases.md` when evaluating decision quality or testing edge cases.

## Required final report

### CHANGEGATE Decision

**Decision:** NO_CHANGE / PARTIAL_FIX / CHANGE_REQUIRED / INVESTIGATE / CLARIFY

**Requested outcome:**

Describe what the user wanted.

**Evidence:**

Summarize relevant code, behavior, tests, or observations.

**Reasoning:**

Explain the decision.

**Action taken:**

Describe the action or explain why no changes were made.

**Verification:**

Report actual tests and results. Identify anything not verified.

## Critical safeguards

- Never invent evidence.
- Never invent test results.
- Never assume an existing function is correct.
- Never ignore partially completed fixes.
- Never modify unrelated files.
- Never silently expand task scope.
- Never reject necessary changes just to minimize edits.
- Never claim this skill provides a security boundary.

The objective is to make the correct change — and avoid the unnecessary one.
