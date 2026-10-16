---
id: ELITEA-4008
title: "Anti-Enumeration — not_shared and not_found Are Indistinguishable at the Wire Level"
priority: critical
type: security
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, anti-enumeration]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-4008: Anti-Enumeration — `not_shared` and `not_found` Are Indistinguishable at the Wire Level

**Module:** Pipelines / Code Node · **Priority:** Critical · **Type:** Security

**Objective:** For the same target personal project, calling the private-secret resolver for (a) a secret that exists but isn't shared and (b) a secret name that doesn't exist at all must produce responses a caller cannot use to tell which secret names exist in a project that isn't theirs — status code and body shape must match.

**Coverage:** TC-CN-05

## Preconditions

- Access to call the private-secret resolver endpoint directly (e.g. via browser devtools/Postman/curl with a valid session)
- Target personal project has one secret `AQA_NOT_SHARED` (exists, unshared) and no secret named `AQA_DOES_NOT_EXIST`

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `GET {base_url}/api/v2/secrets/private_secret/<calling_project_id>/<secret_name>` |
| Case (a) | `secret_name = AQA_NOT_SHARED` (exists, unshared) |
| Case (b) | `secret_name = AQA_DOES_NOT_EXIST` (does not exist) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As a member of a shared project, call the resolver for `AQA_NOT_SHARED` (known to exist, unshared, in another user's personal project). Record status code + full response body. | Response captured. |
| 2 | Call the resolver for `AQA_DOES_NOT_EXIST` (same target identity, guaranteed not to exist). Record status code + full response body. | Response captured. |
| 3 | Diff the two responses byte-for-byte (status code and body content/shape). | Status codes match; body content is identical (same generic denial code/message) — no field or wording differs between the two cases. |

## Expected Final State

No observable signal distinguishes "exists but not shared" from "doesn't exist."

## Pass/Fail Criteria

**Pass:**
- Both responses are indistinguishable (same status code, same body shape/wording)

**Fail:**
- Any difference in status code, error code, or message wording between the two cases — this would let a caller enumerate real secret names in a project they don't own
