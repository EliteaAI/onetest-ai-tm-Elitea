---
id: ELITEA-3202
title: "Regression — unsecret() for Shared Secrets Behaves Exactly as Before"
priority: medium
type: regression
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, regression]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3202: Regression — `unsecret()` for Shared Secrets Unchanged

**Module:** Pipelines / Code Node · **Priority:** Medium · **Type:** Regression

**Objective:** Confirm introducing `get_private_project_secret` had no side effect on the existing `unsecret()` shared-secret resolution path — same signature, same return value, same error behavior on a missing shared secret.

**Coverage:** TC-CN-08

## Preconditions

- A shared-project secret `AQA_TOKEN` exists with a known value
- A shared-project secret name that does not exist, e.g. `AQA_DOES_NOT_EXIST_SHARED`

## Code Node

```python
results = {}
results["existing"] = elitea_client.unsecret('AQA_TOKEN')
try:
    results["missing"] = elitea_client.unsecret('AQA_DOES_NOT_EXIST_SHARED')
except Exception as e:
    results["missing_error"] = type(e).__name__

test_results = results
print(results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `unsecret('AQA_TOKEN')` for an existing shared secret. | Returns the correct known value, same as pre-#5633 behavior. |
| 2 | Call `unsecret()` for a nonexistent shared secret name. | Fails/behaves identically to documented pre-#5633 behavior (same error type/shape). |

## Expected Final State

`unsecret()`'s behavior for shared secrets is byte-for-byte unchanged by the private-secret feature addition.

## Pass/Fail Criteria

**Pass:**
- Existing shared secret resolves to its correct value
- Missing shared secret fails the same way it did before this feature shipped

**Fail:**
- Any change in `unsecret()`'s return value, error type, or error message for shared secrets
