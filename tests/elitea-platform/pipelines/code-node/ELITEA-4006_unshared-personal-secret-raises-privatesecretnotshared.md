---
id: ELITEA-4006
title: "Unshared Personal Secret Raises PrivateSecretNotShared, Node Does Not Succeed With a Wrong/Empty Value"
priority: critical
type: negative
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4006: Unshared Personal Secret Raises `PrivateSecretNotShared`

**Module:** Pipelines / Code Node · **Priority:** Critical · **Type:** Negative

**Objective:** A personal secret that exists but has "Share with other projects" OFF must cause `get_private_project_secret` to fail explicitly — the code node must not complete successfully with an empty or fabricated value.

**Coverage:** TC-CN-03

## Preconditions

- Personal secret `AQA_NOT_SHARED` exists in the caller's personal project
- Its "Share with other projects" opt-in flag is OFF

## Code Node

```python
try:
    value = elitea_client.get_private_project_secret('AQA_NOT_SHARED')
    test_results = {"error": None, "value": value}
except Exception as e:
    test_results = {"error": type(e).__name__, "message": str(e)}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create `AQA_NOT_SHARED` in the personal project, leave opt-in OFF. | Secret exists, unshared. |
| 2 | Run the code node above. | Node executes. |
| 3 | Inspect `test_results`. | `error` is populated (e.g. `PrivateSecretNotShared` or the surfaced equivalent); `value` is `None` — not an empty string and not the shared-project secret's value. |
| 4 | Check the pipeline run's overall status. | Run reflects the failure (errored/handled-exception state), not a silent success. |

## Expected Final State

The run fails explicitly on this call; no value is produced.

## Pass/Fail Criteria

**Pass:**
- Explicit error raised/surfaced
- No value returned
- Run status reflects the failure

**Fail:**
- Any value is returned (including empty string) instead of raising
- Run reports success despite the secret being unshared
