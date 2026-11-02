
# CHANGEGATE

### Think before you change.

CHANGEGATE is an open-source AI coding-agent skill that helps coding agents determine whether a requested software change is actually necessary before modifying code.

Instead of assuming every request requires implementation, CHANGEGATE encourages agents to inspect existing behavior, evaluate evidence, classify the situation, and choose an appropriate action.

**Make the correct change. Avoid the unnecessary one.**

---

## The Problem

AI coding agents can sometimes:

- Modify code that already works.
- Reimplement functionality that already exists.
- Miss partially completed fixes.
- Introduce unrelated changes.
- Make assumptions without inspecting the existing implementation.
- Change more code than the task requires.

These behaviors can waste time, introduce regressions, and reduce developer confidence.

CHANGEGATE is designed to address this problem through a structured decision process before implementation.

## How It Works

CHANGEGATE follows seven steps:

1. **Understand** — Identify the requested outcome.
2. **Inspect** — Examine relevant code, tests, and existing behavior.
3. **Evaluate** — Compare the requested outcome with the current implementation.
4. **Classify** — Select the appropriate decision.
5. **Explain** — Present the evidence and reasoning.
6. **Act** — Implement only when necessary.
7. **Verify** — Check the actual result.

## Five Possible Decisions

| Decision | Meaning |
|---|---|
| NO_CHANGE | The requested outcome already exists. |
| PARTIAL_FIX | Some required behavior exists, but something remains incomplete. |
| CHANGE_REQUIRED | The requested behavior is missing or incorrect. |
| INVESTIGATE | More evidence is required. |
| CLARIFY | The request needs clarification. |

CHANGEGATE does not simply tell agents to avoid editing.

It aims to help them distinguish between situations where editing is unnecessary and situations where editing is essential.

## Supported Coding Agents

CHANGEGATE is designed for compatible coding agents that support the Agent Skills format.

Initial compatibility targets:

- Claude Code
- OpenAI Codex
- Other compatible Agent Skills implementations

Behavior and installation details can differ between agent environments. Compatibility must be tested rather than assumed.

## Installation

### Claude Code

Copy the CHANGEGATE skill folder into your project's:

`.claude/skills/changegate/`

The folder should contain:

`SKILL.md`

You can also install it in your personal skills directory if you want to use it across projects.

### OpenAI Codex

Copy the skill folder into your project's:

`.agents/skills/changegate/`

The folder should contain:

`SKILL.md`

You can also use the personal skills directory supported by your Codex environment.

### Other compatible agents

Consult the agent's documentation for its supported skill directory and activation behavior.

## Usage

After installation, invoke the skill explicitly if your coding agent supports explicit skill invocation.

Example:

> Use CHANGEGATE to inspect this bug report. Determine whether a code change is necessary before implementing anything.

Another example:

> Use CHANGEGATE to check whether this feature already exists in the repository. If it is partially implemented, identify what is missing.

## Example

Imagine a developer reports:

> Fix the login validation bug.

The agent investigates the relevant implementation and discovers that the validation behavior already works correctly.

A conventional implementation-first workflow might still attempt modifications.

CHANGEGATE should instead classify the situation as:

`NO_CHANGE`

It should explain the evidence and avoid unnecessary edits.

However, if validation works only for some cases, CHANGEGATE should identify the missing behavior and select:

`PARTIAL_FIX`

This distinction is central to the project.

## Project Structure

```text
changegate/
│
├── README.md
├── LICENSE
├── CONTRIBUTING.md
│
├── skills/
│   └── changegate/
│       ├── SKILL.md
│       └── references/
│
├── .claude/
│   └── skills/
│       └── changegate/
│           └── SKILL.md
│
├── .agents/
│   └── skills/
│       └── changegate/
│           └── SKILL.md
│
└── evaluations/
    └── README.md
```

## Evaluation

CHANGEGATE is intended to be evaluated against coding agents without the skill.

Important evaluation metrics include:

- Decision accuracy.
- Unnecessary modification rate.
- Missed necessary changes.
- Scope accuracy.
- Evidence quality.
- Additional token and execution cost.

The project will use scenarios involving already-fixed bugs, partially fixed bugs, missing features, incorrect implementations, and ambiguous requests.

Performance claims will only be made when supported by actual evaluation results.

## Design Principles

- Evidence before assumptions.
- Inspection before implementation.
- Preserve working behavior.
- Minimal, task-focused changes.
- Honest verification.
- No invented test results.
- No unnecessary refactoring.
- No premature abstention when a real fix is needed.

## Current Status

**Version:** 0.1.0

**Stage:** Initial development

CHANGEGATE is an evolving open-source project. Its cross-agent compatibility and effectiveness require practical testing.

## Contributing

Contributions, bug reports, evaluation scenarios, documentation improvements, and compatibility feedback are welcome.

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

## License

CHANGEGATE is intended to be released under the MIT License. See [LICENSE](LICENSE).

---

**CHANGEGATE — Think before you change.**
