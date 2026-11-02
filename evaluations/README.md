
# CHANGEGATE — Evaluation Methodology

This directory documents how CHANGEGATE should be evaluated.

The purpose is to determine whether the skill helps coding agents make better decisions about when to change software and when to leave working code alone.

## 1. Evaluation objective

Compare an agent using CHANGEGATE against the same agent operating without CHANGEGATE.

The evaluation should measure decision quality, not merely the number of files changed.

## 2. Initial benchmark

The initial scenario set is maintained in:

`skills/changegate/references/evaluation-cases.md`

It contains 10 manually authored scenarios covering:

- Already implemented behavior.
- Previously fixed behavior.
- Partially implemented features.
- Missing features.
- Incorrect implementations.
- Insufficient evidence.
- Ambiguous requirements.
- Unrelated cleanup opportunities.
- Partial validation.
- Conflicting requirements.

These cases are a starting point, not a statistically representative benchmark.

## 3. Recommended comparison procedure

For every scenario:

1. Prepare the same repository state for both runs.
2. Use the same coding agent and model.
3. Provide the same user request and relevant context.
4. Run one trial without CHANGEGATE.
5. Run another trial with CHANGEGATE enabled.
6. Record the agent's decision, explanation, edits, and verification.
7. Compare both outcomes against the expected decision and scenario requirements.

Keep the environment and instructions as consistent as possible.

Avoid giving one run additional information that the other run does not receive.

## 4. Metrics

Record these measurements:

| Metric | What it measures |
|---|---|
| Decision accuracy | Whether the agent selected the expected decision category |
| Unnecessary edit rate | How often the agent changed code when no change was needed |
| Missed change rate | How often the agent failed to make a necessary change |
| Partial-fix accuracy | Whether the agent correctly identified remaining work |
| Evidence quality | Whether decisions were supported by inspected evidence |
| Verification honesty | Whether test results and limitations were reported accurately |
| Scope control | Whether unrelated changes were avoided |

Decision accuracy alone is insufficient. An agent that never changes anything might avoid unnecessary edits but fail to fix genuine problems.

## 5. Suggested initial targets

These are proposed engineering targets, not measured results or guarantees:

- At least 90% decision accuracy.
- No more than 5% unnecessary edits on NO_CHANGE scenarios.
- No more than 10% missed necessary changes.
- No fabricated test results.
- No unrelated edits in scenarios where no change is required.

Targets should be reviewed as the benchmark grows.

## 6. Recording results

For each trial, record:

- Scenario ID.
- Agent and model.
- Whether CHANGEGATE was enabled.
- Expected decision.
- Actual decision.
- Files changed.
- Tests or checks executed.
- Test outcomes.
- Whether the result was correct.
- Notes explaining any failure.

Keep baseline and CHANGEGATE results separate.

## 7. Limitations

The initial 10 scenarios are manually authored and may not represent real-world coding tasks.

Results from a small number of scenarios cannot establish broad effectiveness.

A credible evaluation should eventually include:
- More scenarios from real repositories.
- Multiple programming languages and frameworks.
- Different coding agents and models.
- Repeated trials to account for model variability.
- Independent review of borderline decisions.

## 8. Reporting rule

Publish actual results, including failures.

Never describe proposed targets as achieved results.

Never claim that CHANGEGATE improves coding-agent performance until controlled comparisons provide supporting evidence.
