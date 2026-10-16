---
id: ELITEA-4007
title: "No Silent Fallback From Private Secret to a Same-Named Shared Secret (D5)"
priority: critical
type: security
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, no-fallback]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4007: No Silent Fallback From Private Secret to a Same-Named Shared Secret (D5)

**Module:** Pipelines / Code Node · **Priority:** Critical · **Type:** Security

**Objective:** Verify `get_private_project_secret` never silently substitutes a same-named shared-project secret — neither when the personal secret is shared with a different value (must resolve to the personal value, proven via a fingerprint diff) nor when the personal secret is unshared (must raise, never fall through to the shared value). This is the design's explicitly named critical security case (D5) — a silent fallback here means the pipeline runs as the wrong account's secret.

**Coverage:** TC-CN-04

## Preconditions

- A shared-project secret `AQA_TOKEN` exists, value `S`
- A personal-project secret `AQA_TOKEN` exists (same name), value `P`, `P != S`
- Use disposable, non-sensitive dummy strings for `S` and `P` — Variant A below intentionally surfaces both raw values in its output, so do not use real credentials for this test.

## Variant A — personal secret shared, values differ

**Precondition:** personal `AQA_TOKEN` share flag = ON.

```python
import hashlib

def fp(value):
    # Non-revealing identity check: same value => same fingerprint
    if value is None:
        return None
    return hashlib.sha256(value.encode()).hexdigest()[:8]

shared_value = elitea_client.unsecret('AQA_TOKEN')
private_value = elitea_client.get_private_project_secret('AQA_TOKEN')

result = {
    "shared_fp": shared_value,
    "private_fp": private_value,
    "private_len": len(private_value) if private_value else 0,
    "private_differs_from_shared": fp(private_value) != fp(shared_value),
}
test_results = result
print(result)

test_results
```

**Expected:** `private_differs_from_shared == True`; `private_value` corresponds to `P`, not `S`.

## Variant B — personal secret unshared

**Precondition:** toggle the same `AQA_TOKEN`'s share flag to OFF (value `P` unchanged, shared secret `S` unchanged).

```python
import hashlib

def fp(value):
    if value is None:
        return None
    return hashlib.sha256(value.encode()).hexdigest()[:8]

shared_value = elitea_client.unsecret('AQA_TOKEN')
try:
    private_value = elitea_client.get_private_project_secret('AQA_TOKEN')
    test_results = {"error": None, "fell_back_to_shared": fp(private_value) == fp(shared_value)}
except Exception as e:
    test_results = {"error": type(e).__name__, "fell_back_to_shared": False}
print(test_results)
test_results
```

**Expected:** `error` is populated (not `None`); `fell_back_to_shared` never becomes `True`.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set up shared secret `S` and personal secret `P` (`P != S`), personal share flag = ON. Run Variant A. | `private_differs_from_shared == True`. |
| 2 | Toggle the personal secret's share flag to OFF, leaving both secrets' values otherwise unchanged. Run Variant B. | Call raises; `error` is populated; no fallback value is returned. |

## Expected Final State

Personal secret resolution is never observably equal to the shared secret's value, whether shared (different value proven) or unshared (raises instead of falling back).

## Pass/Fail Criteria

**Pass:**
- Variant A proves the personal value is returned, not the shared one
- Variant B proves no exception-free fallback occurs

**Fail:**
- Variant A's `private_differs_from_shared` is `False` while the flag is ON (fallback to shared)
- Variant B returns `S`'s value instead of raising (`fell_back_to_shared` ends up `True`)
