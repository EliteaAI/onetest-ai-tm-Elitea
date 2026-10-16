---
id: ELITEA-4004
title: "get_private_project_secret Returns Each Caller's Own Value, Not the Other User's"
priority: critical
type: functional
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, per-caller-resolution]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4004: `get_private_project_secret` Returns Each Caller's Own Value, Not the Other User's

**Module:** Pipelines / Code Node · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `get_private_project_secret` resolves per the identity of the user actually running the pipeline — User A and User B running the identical shared pipeline/code node each receive their own personal-project secret value, never each other's.

**Coverage:** TC-CN-01

## Preconditions

- Two users, User A and User B, each with their own personal project
- A shared project both A and B are members of, containing a pipeline with a Code node
- User A's personal project has a secret `AQA_TOKEN` = `value_A`, "Share with other projects" = ON
- User B's personal project has a secret `AQA_TOKEN` = `value_B` (different from `value_A`), "Share with other projects" = ON

## Test Data

| Field | Value |
|-------|-------|
| Secret name | `AQA_TOKEN` |
| User A's value | e.g. `aqa-a-1111` |
| User B's value | e.g. `aqa-b-2222` (must differ from A's) |

## Code Node

```python
value = elitea_client.get_private_project_secret('AQA_TOKEN')
test_results = {"value": value, "length": len(value) if value else 0}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure `AQA_TOKEN` in A's and B's personal projects with distinct values, both shared. | Both secrets created and opted in. |
| 2 | As User A, run the shared pipeline. Inspect the code node's output/state. | Output value equals `value_A`. |
| 3 | As User B, run the same shared pipeline (no config changes in between). Inspect output. | Output value equals `value_B`, not `value_A`. |
| 4 | Compare the two run outputs directly. | The two outputs differ and each matches its own owner's secret — no cross-user leakage. |

## Expected Final State

Each run's resolved secret matches only the identity that executed it.

## Pass/Fail Criteria

**Pass:**
- A's run returns `value_A`; B's run returns `value_B`
- Values are never swapped, cached from the other user's run, or replaced by a shared-project value

**Fail:**
- Either run returns the other user's value
- A run returns a stale value from a prior run by a different user
- Either run returns the shared-project secret instead of a personal one
