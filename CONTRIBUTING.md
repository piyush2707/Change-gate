
# Contributing to CHANGEGATE

Thank you for your interest in contributing to CHANGEGATE!

CHANGEGATE aims to help AI coding agents make better decisions before modifying software.

We welcome contributions that improve its accuracy, reliability, usability, and compatibility.

## Ways to Contribute

You can contribute by:

- Reporting bugs or unexpected agent behavior.
- Suggesting improvements to decision rules.
- Adding realistic evaluation scenarios.
- Improving documentation.
- Testing compatibility with coding agents.
- Identifying cases where CHANGEGATE makes incorrect decisions.
- Improving installation instructions.

## Core Contribution Principles

Every contribution should support these principles:

1. Evidence before assumptions.
2. Inspection before implementation.
3. Preserve working behavior.
4. Avoid unnecessary modifications.
5. Do not ignore partially fixed problems.
6. Never invent verification results.
7. Keep changes focused on the user's request.

## Reporting Issues

When reporting an issue, include:

- The coding agent used.
- The task or prompt provided.
- The relevant repository context, if shareable.
- CHANGEGATE's decision.
- What the correct decision should have been.
- Evidence explaining why the decision was incorrect.

Do not include passwords, API keys, private credentials, or confidential project information.

## Proposing Improvements

Before proposing a major change:

1. Explain the problem.
2. Describe the proposed improvement.
3. Provide a realistic example.
4. Explain how the improvement can be evaluated.
5. Consider possible negative effects.

Avoid adding complexity without demonstrating its value.

## Evaluation Contributions

Useful evaluation scenarios include:

- A bug that is already fixed.
- A bug that is partially fixed.
- A genuinely broken implementation.
- A missing feature.
- An ambiguous request.
- A task where investigation is required before implementation.

Each scenario should include:

- Initial repository state.
- User request.
- Expected decision.
- Evidence supporting the expected decision.
- Expected behavior after the decision.

## Pull Requests

When submitting a pull request:

- Keep changes focused.
- Explain why the change is necessary.
- Update relevant documentation.
- Include evaluation examples when appropriate.
- Do not claim tests passed unless they were actually run.

## Compatibility

CHANGEGATE is designed for compatible Agent Skills implementations.

Compatibility reports should identify the agent, its version when known, installation method, invocation method, and observed behavior.

## Project Direction

CHANGEGATE is not intended to prevent all code changes.

Its purpose is to help coding agents determine when a change is necessary and when it is not.

Contributions should preserve that central purpose.

Thank you for helping improve CHANGEGATE!
