
---
name: changegate
description: Evaluate whether a requested software change is necessary before modifying code. Distinguish already-correct, partially fixed, broken, missing, and unclear behavior. Use when handling bug reports, feature requests, code improvements, refactoring requests, or other software changes.
---

# CHANGEGATE

Think before you change.

Your responsibility is to determine whether a requested software change is necessary before implementing it.

Do not assume that every request requires a code modification.

## Core principles

1. Understand the requested outcome before editing.
2. Inspect relevant existing code before proposing changes.
3. Use evidence rather than assumptions.
4. Preserve working behavior.
5. Avoid unrelated modifications and unnecessary refactoring.
6. Never confuse an already-fixed issue with a partially fixed issue.
7. Never claim something was tested or verified unless you actually did it.
8. Do not modify files until you have established that a change is necessary, unless the user explicitly requests a different workflow.

## Reference materials

This skill includes additional reference documents.

Read `references/decision-rules.md` before making a decision.

Use it to understand the five decision categories, evidence standards, scope control, and verification requirements.

Read `references/evaluation-cases.md` when evaluating decision quality, checking edge cases, or developing additional benchmark scenarios.

Do not assume that reading a reference document proves that its requirements have been satisfied.

Apply the rules to the actual repository and available evidence.

## Decision workflow

### 1. Understand

Identify:

- What outcome does the user want?
- What behavior currently exists?
- What behavior should exist?
- What conditions must be satisfied?
- What files or components are likely relevant?

If the request is ambiguous, identify the uncertainty.

### 2. Inspect

Before changing code:

- Read the relevant implementation.
- Inspect related functions and components.
- Examine existing tests where available.
- Check relevant configuration and documentation.
- Search for existing implementations of the requested behavior.
- Inspect relevant project history when useful.

Do not inspect unrelated repository areas without a reason.

### 3. Evaluate

Compare the requested outcome with actual existing behavior.

Determine:

- Does the requested behavior already work?
- Is the implementation completely correct?
- Is it partially implemented?
- Is there a real defect?
- Is the requested functionality missing?
- Is there insufficient evidence?
- Does the request require clarification?

Do not treat the existence of code as proof that the requested behavior works.

### 4. Classify

Select exactly one primary decision:

**NO_CHANGE**

The requested outcome already exists and available evidence supports that conclusion.

**PARTIAL_FIX**

Some requested behavior works, but identifiable requirements remain incomplete.

**CHANGE_REQUIRED**

The requested behavior is absent or demonstrably incorrect.

**INVESTIGATE**

Available evidence is insufficient to make a reliable decision.

**CLARIFY**

The request contains ambiguity that materially affects implementation.

Use `references/decision-rules.md` for the complete definitions and safeguards.

### 5. Explain

Before implementation, report:

- The decision.
- What you inspected.
- What evidence supports the decision.
- What remains uncertain.
- Whether a code modification is necessary.

Keep the explanation concise and specific.

### 6. Act

Follow the selected decision.

- NO_CHANGE: Stop without unnecessary code edits.
- PARTIAL_FIX: Complete only the missing requirements.
- CHANGE_REQUIRED: Implement the smallest suitable change.
- INVESTIGATE: Gather more evidence without premature modifications.
- CLARIFY: Ask the user for the missing information.

Respect user instructions and the permissions of the coding environment.

Never claim this skill provides a hard security boundary or overrides host permissions.

### 7. Verify

When modifications are made:

- Inspect the resulting diff.
- Run relevant tests when available.
- Check for unintended changes.
- Verify the requested behavior using available evidence.
- Report tests that could not be run.

When no modification is necessary, explain what evidence supports the NO_CHANGE decision.

## Required final report

Use this format:

### CHANGEGATE Decision

**Decision:** NO_CHANGE / PARTIAL_FIX / CHANGE_REQUIRED / INVESTIGATE / CLARIFY

**Requested outcome:**

Describe what the user wanted.

**Evidence:**

Summarize relevant code, behavior, tests, or observations.

**Reasoning:**

Explain why the selected decision is appropriate.

**Action taken:**

Describe what you did, or explain why no changes were made.

**Verification:**

Report actual tests and results. Clearly identify anything not verified.

## Critical safeguards

- Never invent evidence.
- Never report a test as passing if it was not run.
- Never assume a bug is fixed merely because a related function exists.
- Never reject a partially fixed issue without identifying what remains broken.
- Never make unrelated improvements just because an opportunity is visible.
- Never silently expand the scope of the user's request.
- When uncertain, investigate or clarify rather than guessing.

## Success criterion

The objective is not to minimize code changes at all costs.

The objective is to make the correct change — and avoid the incorrect one.
