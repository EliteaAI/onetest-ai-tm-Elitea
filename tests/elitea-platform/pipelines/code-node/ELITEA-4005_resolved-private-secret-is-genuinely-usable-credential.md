---
id: ELITEA-4005
title: "Resolved Private Secret Is a Genuinely Usable Credential, Not Just a Non-Empty String"
priority: high
type: integration
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4005: Resolved Private Secret Is a Genuinely Usable Credential

**Module:** Pipelines / Code Node · **Priority:** High · **Type:** Integration

**Objective:** Confirm the value returned by `get_private_project_secret` actually functions as a valid credential against a real external system, not merely a non-empty placeholder string.

**Coverage:** TC-CN-02

## Preconditions

- User has a real, currently-valid personal access token (or equivalent credential) for an external service, scoped to that user's own account (e.g. a GitHub PAT)
- That token is stored as a private, shared secret (`GH_PAT`) in the user's personal project

## Test Data

| Field | Value |
|-------|-------|
| Secret name | `GH_PAT` |
| External endpoint | `https://api.github.com/user` |

## Code Node

```python
import requests

token = elitea_client.get_private_project_secret('GH_PAT')
resp = requests.get('https://api.github.com/user', headers={'Authorization': f'Bearer {token}'})
test_results = {
    "status_code": resp.status_code,
    "login": resp.json().get('login') if resp.status_code == 200 else None,
}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Store the user's real PAT as a private, shared secret named `GH_PAT`. | Secret saved, opt-in ON. |
| 2 | Run the code node above from a pipeline in a shared project. | Node executes without error. |
| 3 | Inspect `test_results.status_code` and `test_results.login`. | `status_code == 200` and `login` matches the actual owner of the PAT. |

## Expected Final State

The external API call authenticates successfully as the secret's true owner.

## Pass/Fail Criteria

**Pass:**
- 200 response
- Returned identity matches the token's real owner

**Fail:**
- 401/403 (token resolved to a garbage/wrong value)
- `login` does not match the expected owner (wrong user's token was resolved)
