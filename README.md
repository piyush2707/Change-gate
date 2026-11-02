CHANGEGATE

Think before you change.

CHANGEGATE is an open-source AI coding-agent skill that helps coding agents determine whether a requested software change is actually necessary before modifying code.

Instead of assuming every request requires implementation, CHANGEGATE encourages agents to inspect existing behavior, evaluate evidence, classify the situation, and choose an appropriate action.

Make the correct change. Avoid the unnecessary one.

---

The Problem

AI coding agents can sometimes:

- Modify code that already works.
- Reimplement functionality that already exists.
- Miss partially completed fixes.
- Introduce unrelated changes.
- Make assumptions without inspecting the implementation.
- Change more code than the task requires.

These behaviors can waste time, introduce regressions, and reduce developer confidence.

CHANGEGATE introduces a structured decision process before implementation.

How It Works

CHANGEGATE follows seven steps:

1. Understand — Identify the requested outcome.
2. Inspect — Examine relevant code, tests, and existing behavior.
3. Evaluate — Compare the requested outcome with the current implementation.
4. Classify — Select the appropriate decision.
5. Explain — Present the evidence and reasoning.
6. Act — Implement only when necessary.
7. Verify — Check the actual result.

Five Possible Decisions

Decision| Meaning
"NO_CHANGE"| The requested outcome already exists.
"PARTIAL_FIX"| Some required behavior exists, but something remains incomplete.
"CHANGE_REQUIRED"| The requested behavior is missing or incorrect.
"INVESTIGATE"| More evidence is required.
"CLARIFY"| The request needs clarification.

CHANGEGATE does not simply tell agents to avoid editing. It helps distinguish unnecessary changes from necessary ones.

Supported Coding Agents

Initial compatibility targets:

- Claude Code
- OpenAI Codex
- Other compatible Agent Skills implementations

Compatibility and behavior must be tested in each agent environment rather than assumed.

Installation

Important: Install the complete "changegate" skill folder, including "SKILL.md" and its "references/" directory. Copying only "SKILL.md" is not a complete installation.

Claude Code

Copy the contents of:

".claude/skills/changegate/"

into your project's:

".claude/skills/changegate/"

The installed folder must contain:

changegate/
├── SKILL.md
└── references/
    ├── decision-rules.md
    └── evaluation-cases.md

OpenAI Codex

Copy the contents of:

".agents/skills/changegate/"

into your project's:

".agents/skills/changegate/"

The installed folder must contain:

changegate/
├── SKILL.md
└── references/
    ├── decision-rules.md
    └── evaluation-cases.md

Other compatible agents

Consult the agent's documentation for its supported skill directory, installation procedure, and activation behavior.

Usage

After installation, invoke CHANGEGATE explicitly if your coding agent supports skill invocation.

Example:

«Use CHANGEGATE to inspect this bug report. Determine whether a code change is necessary before implementing anything.»

Another example:

«Use CHANGEGATE to check whether this feature already exists in the repository. If it is partially implemented, identify what is missing.»

Example

Imagine a developer reports:

«Fix the login validation bug.»

The agent investigates the relevant implementation and discovers that the validation behavior already works correctly.

CHANGEGATE should classify the situation as:

"NO_CHANGE"

It should explain the evidence and avoid unnecessary edits.

However, if validation works only for some cases, CHANGEGATE should identify the missing behavior and select:

"PARTIAL_FIX"

This distinction is central to the project.

## Project Structure

```text
Change-gate/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
│
├── skills/
│   └── changegate/
│       ├── SKILL.md
│       └── references/
│           ├── decision-rules.md
│           └── evaluation-cases.md
│
├── .claude/
│   └── skills/
│       └── changegate/
│           ├── SKILL.md
│           └── references/
│               ├── decision-rules.md
│               └── evaluation-cases.md
│
├── .agents/
│   └── skills/
│       └── changegate/
│           ├── SKILL.md
│           └── references/
│               ├── decision-rules.md
│               └── evaluation-cases.md
│
└── evaluations/
    └── README.md
```

The root `skills/` directory is the canonical skill distribution. The `.claude/` and `.agents/` directories provide agent-specific installation copies.

The root "skills/" directory is the canonical skill distribution. The ".claude/" and ".agents/" directories provide agent-specific installation copies.

Evaluation

CHANGEGATE is designed to be evaluated against coding agents operating without the skill.

Important evaluation metrics include:

- Decision accuracy.
- Unnecessary modification rate.
- Missed necessary changes.
- Partial-fix accuracy.
- Evidence quality.
- Verification honesty.
- Scope control.

The initial evaluation set contains 10 manually authored scenarios.

See ""evaluations/README.md"" (evaluations/README.md) for the evaluation methodology.

No performance improvement is claimed until controlled evaluations provide supporting evidence.

Design Principles

- Evidence before assumptions.
- Inspection before implementation.
- Preserve working behavior.
- Minimal, task-focused changes.
- Honest verification.
- No invented test results.
- No unnecessary refactoring.
- No premature abstention when a real fix is needed.

Current Status

- Project version: 0.1.0
- Stage: Initial development
- Release: Not yet published

CHANGEGATE is an evolving open-source project. Its cross-agent compatibility, usability, and effectiveness require practical testing.

Contributing

Contributions, bug reports, evaluation scenarios, documentation improvements, and compatibility feedback are welcome.

See ""CONTRIBUTING.md"" (CONTRIBUTING.md) for contribution guidelines.

License

CHANGEGATE is licensed under the MIT License. See ""LICENSE"" (LICENSE).

---

CHANGEGATE — Think before you change.
