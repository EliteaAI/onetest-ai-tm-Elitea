---
id: ELITEA-3201
title: "default= Parameter Suppresses All Three Refusal Reasons, Including default=None"
priority: high
type: functional
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3201: `default=` Parameter Suppresses All Three Refusal Reasons

**Module:** Pipelines / Code Node · **Priority:** High · **Type:** Functional

**Objective:** Confirm `get_private_project_secret(name, default=...)` swallows every refusal reason (`no_personal_project`, `not_shared`, `not_found`) and returns the given default instead of raising — and that `default=None` is honored as an explicit default, not treated as "no default given."

**Coverage:** TC-CN-07

## Preconditions

- A secret name that doesn't exist anywhere (`not_found` case)
- A secret that exists but is unshared (`not_shared` case, e.g. `AQA_NOT_SHARED` from ELITEA-3196)
- A run context with no resolvable personal project (`no_personal_project` case — reuse ELITEA-3199's setup)

## Code Node

```python
results = {}
for name, secret_name in [
    ("not_found", "AQA_DOES_NOT_EXIST"),
    ("not_shared", "AQA_NOT_SHARED"),
]:
    results[name] = elitea_client.get_private_project_secret(secret_name, default=None)

results["explicit_default"] = elitea_client.get_private_project_secret('AQA_DOES_NOT_EXIST', default='fallback-value')

test_results = results
print(results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the code above against a `not_found` secret name with `default=None`. | Returns `None`, no exception raised. |
| 2 | Run against a `not_shared` secret with `default=None`. | Returns `None`, no exception raised. |
| 3 | Run `get_private_project_secret` against a missing-personal-project context (ELITEA-3199's setup) with `default=None`. | Returns `None`, no exception raised (`NoPersonalProject` also suppressed). |
| 4 | Run with an explicit non-`None` default (e.g. `'fallback-value'`) against a missing secret. | Returns `'fallback-value'` exactly, not `None` and not an exception. |

## Expected Final State

Every refusal path returns the caller-supplied default instead of raising, and the code node continues executing normally.

## Pass/Fail Criteria

**Pass:**
- Every refusal case returns the given default (`None` or otherwise) with no exception, and the code node continues executing

**Fail:**
- Any refusal case still raises despite `default=` being passed
- `default=None` is treated as if no default were given (i.e. it still raises)
