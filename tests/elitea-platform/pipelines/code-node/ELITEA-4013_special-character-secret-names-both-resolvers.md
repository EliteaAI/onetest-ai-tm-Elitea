---
id: ELITEA-4013
title: "Secret Names With Special Characters Resolve Correctly via Both unsecret() and get_private_project_secret()"
priority: medium
type: functional
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, edge-case]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4013: Special-Character Secret Names on Both Resolvers

**Module:** Pipelines / Code Node · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm secret names containing `/`, spaces, unicode, and `%` resolve correctly (or fail consistently, if such names are actually rejected at creation time) through both `unsecret()` (shared) and `get_private_project_secret()` (private) — no path-parsing or encoding bug specific to either resolver.

**Coverage:** TC-CN-09

## Preconditions

- Attempt to create both a shared and a personal secret for each name below. If secret creation itself rejects a given name, record that as the outcome for that name and skip the resolution step for it.

## Test Data

| Name | Notes |
|------|-------|
| `path/style` | Contains `/` — the private endpoint is path-based (`.../private_secret/<project_id>/<secret>`), so `/` in the name itself is the primary risk. |
| `with space` | Contains a literal space. |
| `ünïcödé` | Non-ASCII/unicode characters. |
| `percent%20name` | Literal `%` characters (not URL-encoded space — the literal text). |

## Code Node

```python
names = ["path/style", "with space", "ünïcödé", "percent%20name"]
results = {}
for n in names:
    try:
        results[n] = {
            "shared": elitea_client.unsecret(n),
            "private": elitea_client.get_private_project_secret(n),
        }
    except Exception as e:
        results[n] = {"error": type(e).__name__}
test_results = results
print(results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Attempt to create a shared and a personal secret under each name in Test Data. | Either both succeed with the same acceptance/rejection behavior, or creation is rejected consistently — record actual behavior. |
| 2 | For each name accepted at creation, run the code node above. | Both `unsecret()` and `get_private_project_secret()` return the correct value for that name — no truncation at `/` or `%`, no silent mismatch between the two resolvers for the same name. |
| 3 | Compare shared vs. private resolution behavior per name. | Both resolvers behave identically for a given name (both succeed and return correct values, or both fail the same way) — no resolver-specific bug. |

## Expected Final State

Special characters in secret names are handled consistently between the shared and private resolution paths; no name causes one resolver to succeed and the other to silently return a wrong/truncated value.

## Pass/Fail Criteria

**Pass:**
- Each name's value round-trips correctly through both resolvers, or both resolvers reject it consistently

**Fail:**
- One resolver returns a truncated/wrong value for a name while the other returns the correct value (path-parsing discrepancy) — especially for `path/style` against the path-based private endpoint
- Silent data corruption (wrong value returned without an error) for any name
