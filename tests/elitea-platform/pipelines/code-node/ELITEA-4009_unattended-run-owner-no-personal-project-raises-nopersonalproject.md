---
id: ELITEA-4009
title: "Unattended Run — Owner Has No Personal Project Raises NoPersonalProject, No Fallback to Another Identity"
priority: high
type: negative
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, unattended-runs]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4009: Unattended Run — Owner Has No Personal Project Raises `NoPersonalProject`

**Module:** Pipelines / Code Node · **Priority:** High · **Type:** Negative

**Objective:** A scheduled/webhook-triggered run has no live user session; it must resolve against the pipeline/application owner's identity. If that owner has no personal project, the call must fail with `NoPersonalProject` — it must never silently resolve against some other identity (e.g. whoever last edited the pipeline, or a default/fallback account).

**Coverage:** TC-CN-06

## Preconditions

- Pipeline owned by a user/application identity with no personal project (or with the personal-project association removed for test purposes)
- Code node calls `get_private_project_secret`
- Pipeline has a schedule or webhook trigger configured

## Code Node

```python
try:
    value = elitea_client.get_private_project_secret('AQA_TOKEN')
    test_results = {"error": None, "value_present": value is not None}
except Exception as e:
    test_results = {"error": type(e).__name__}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the pipeline owner identity has no personal project. | Confirmed via account/project admin view. |
| 2 | Trigger the pipeline via its schedule/webhook (not an interactive run). | Run starts unattended. |
| 3 | Inspect the code node's result / run logs. | `error == NoPersonalProject` (or the surfaced equivalent); `value_present` is never `true`. |

## Expected Final State

The unattended run fails explicitly with `NoPersonalProject`; no secret value is ever produced.

## Pass/Fail Criteria

**Pass:**
- Run fails explicitly with `NoPersonalProject`

**Fail:**
- Run succeeds with any value
- Run fails with a different/generic error that obscures the real cause
