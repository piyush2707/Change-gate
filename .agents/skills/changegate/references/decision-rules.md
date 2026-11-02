# CHANGEGATE — Decision Rules

These rules define how CHANGEGATE classifies whether a requested software change is necessary.

## 1. Core principle

Do not assume that a requested change is necessary merely because the user requested it.

Inspect the relevant implementation and available evidence before deciding.

The goal is to make the smallest correct change—not to avoid changes at all costs.

## 2. The five decision categories

### NO_CHANGE

Use when the requested behavior already works correctly.

Requirements:
- Inspect the relevant implementation.
- Check available tests or other relevant evidence.
- Confirm that the requested outcome is already satisfied.
- Explain why additional changes are unnecessary.

Do not modify files merely to demonstrate activity.

### PARTIAL_FIX

Use when some of the requested behavior already exists, but a specific gap remains.

Requirements:
- Identify what already works.
- Identify what is incomplete or incorrect.
- Isolate the smallest remaining change.
- Preserve correct existing behavior.

Do not rewrite a working implementation unnecessarily.

### CHANGE_REQUIRED

Use when evidence establishes that the requested behavior is missing, broken, or incorrect.

Requirements:
- Identify the specific failure or missing behavior.
- Explain why the existing implementation does not satisfy the request.
- Implement the smallest appropriate correction when authorized.
- Verify the result using available checks.

### INVESTIGATE

Use when the available evidence is insufficient to make a reliable decision.

Examples:
- Relevant files cannot be accessed.
- A required dependency or service is unavailable.
- The behavior depends on an external system that cannot be inspected.
- Available tests do not establish the actual behavior.

Requirements:
- State what was inspected.
- Identify the missing evidence.
- Perform safe, relevant investigation when possible.
- Do not present assumptions as confirmed findings.

### CLARIFY

Use when the request has multiple materially different interpretations or lacks a necessary requirement.

Requirements:
- Identify the ambiguity.
- Explain why it affects the implementation.
- Ask the smallest necessary clarification.
- Do not silently choose a consequential interpretation.

## 3. Evidence hierarchy

Prefer direct evidence over assumptions.

Use evidence in roughly this order:

1. Reproduced behavior or a reliable failing test.
2. Relevant implementation and its execution path.
3. Existing tests and their actual results.
4. Configuration, dependencies, and documented contracts.
5. Logs, error messages, and available runtime information.
6. Documentation and comments.
7. Inference or assumptions.

Documentation and comments can be outdated. Verify important claims against the implementation when possible.

## 4. Partial-fix discipline

A partially implemented feature must not automatically be classified as complete or broken.

Determine:
- Which requirements are already satisfied?
- Which requirements remain unsatisfied?
- Is the remaining gap relevant to the user's request?
- Can the gap be fixed without replacing working behavior?

Classify as PARTIAL_FIX when meaningful work remains and the existing implementation already satisfies part of the request.

## 5. Verification discipline

After making a change:

- Run relevant available tests or checks.
- Inspect the resulting diff.
- Confirm that the change addresses the identified gap.
- Check for unintended changes when practical.

Never claim a test passed unless it was actually executed and passed.

If verification cannot be performed, state that limitation clearly.

## 6. Scope control

- Do not refactor unrelated code.
- Do not add dependencies without a demonstrated need.
- Do not change public interfaces unnecessarily.
- Do not replace working implementations simply because another approach looks cleaner.
- Do not expand the request into unrelated improvements.

## 7. Final decision report

Report:

- **Decision:** one of the five categories.
- **Evidence:** what was actually inspected or tested.
- **Finding:** what already works and what does not.
- **Action:** what was changed, or why no change was made.
- **Verification:** checks performed and their actual results.
- **Limitations:** anything important that remains unverified.

A concise, evidence-backed explanation is better than a confident but unsupported conclusion.
