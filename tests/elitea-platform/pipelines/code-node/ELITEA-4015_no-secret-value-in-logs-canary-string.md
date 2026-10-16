---
id: ELITEA-4015
title: "No Private Secret Value Ever Appears in Logs — Canary String Check"
priority: critical
type: security
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, audit-logging]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4015: No Private Secret Value Ever Appears in Logs

**Module:** Pipelines / Code Node · **Priority:** Critical · **Type:** Security

**Objective:** Confirm that resolving a private project secret never writes the actual secret value into any application/audit log — logs must only carry `has_value=` style markers, never the raw value, even under error conditions or verbose/debug logging.

**Coverage:** Extra — no secret value in logs

## Preconditions

- Access to application logs / audit logs for the environment under test (log aggregator, file tail, or admin log viewer)
- A personal secret set to a unique, easily greppable canary value, e.g. `AQA-CANARY-8f3c1e`

## Test Data

| Field | Value |
|-------|-------|
| Secret name | `AQA_CANARY_SECRET` |
| Secret value | `AQA-CANARY-8f3c1e` (disposable, unique, greppable — never a real credential) |

## Code Node

```python
value = elitea_client.get_private_project_secret('AQA_CANARY_SECRET')
test_results = {"has_value": value is not None}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create personal secret `AQA_CANARY_SECRET` = `AQA-CANARY-8f3c1e`, shared = ON. | Secret created. |
| 2 | Run the code node above (success case). | Resolves successfully; code node output shows only `has_value: true`, never the raw string. |
| 3 | Toggle share flag OFF and re-run to force a `PrivateSecretNotShared` error path. | Call raises as expected. |
| 4 | Grep all available logs (app logs, audit logs, error logs, run logs) for the literal canary string `AQA-CANARY-8f3c1e` across both steps 2 and 3. | Zero matches anywhere. |
| 5 | Grep logs for `has_value=` (or equivalent marker) around the relevant timestamps. | Marker is present, confirming logging is active but non-revealing. |

## Expected Final State

The canary value never appears in any log line, in either the success path or the error path; only boolean/marker-style presence indicators are logged.

## Pass/Fail Criteria

**Pass:**
- Canary string is absent from every log source checked, across both success and error paths
- `has_value=`-style markers are present, confirming logging isn't simply disabled

**Fail:**
- The raw canary value appears in any log line (app, audit, error, or run log), in success or error path
