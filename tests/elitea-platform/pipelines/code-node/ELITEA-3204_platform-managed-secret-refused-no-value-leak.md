---
id: ELITEA-3204
title: "Platform-Managed/Default Secret via get_private_project_secret Is Refused Generically, No Value Leak"
priority: high
type: security
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, default-secrets]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3204: Platform-Managed/Default Secret Refused Generically via `get_private_project_secret`

**Module:** Pipelines / Code Node · **Priority:** High · **Type:** Security

**Objective:** Confirm requesting a platform-managed/default secret key (subject to `default_secret_keys` / `ignore_default_secret_api` guard) through `get_private_project_secret` is refused with the same generic error contract as any other refusal — not a distinct error that reveals the key is platform-managed, and never returns the actual platform-managed value.

**Coverage:** Extra — platform-managed/default secret guard

## Preconditions

- Identify a secret key name that is platform-managed/default per `default_secret_keys` (or equivalent internal config) in the target environment

## Code Node

```python
try:
    value = elitea_client.get_private_project_secret('<default_secret_key_name>')
    test_results = {"error": None, "value_leaked": value is not None}
except Exception as e:
    test_results = {"error": type(e).__name__, "message": str(e)}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_private_project_secret` with a known platform-managed/default secret key name. | Call fails. |
| 2 | Inspect the error type/message returned. | Generic refusal (same shape as `PrivateSecretNotShared`/`PrivateSecretNotFound`/`PrivateSecretError`) — nothing in the error identifies the key as platform-managed specifically. |
| 3 | Confirm no value is present anywhere in the result. | `value_leaked` is never `true`; the actual platform-managed secret value never appears in the code node output or logs. |

## Expected Final State

Platform-managed/default secrets are unreachable via the private-secret path, refused with the standard generic error contract, and their values never surface.

## Pass/Fail Criteria

**Pass:**
- Call fails with the standard generic refusal, no distinguishing detail, no value ever returned

**Fail:**
- The platform-managed value is returned
- The error message/type reveals that the key is specifically platform-managed (a distinguishable signal an attacker could use to enumerate protected keys)
