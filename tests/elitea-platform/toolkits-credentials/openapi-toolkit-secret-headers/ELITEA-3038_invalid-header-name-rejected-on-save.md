---
id: ELITEA-3038
title: "Invalid Header Name (Space, Colon, or Blank) Is Rejected on Save With a Clear Error"
priority: high
type: negative
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, nfr:validation, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3038: Invalid Header Name (Space, Colon, or Blank) Is Rejected on Save With a Clear Error

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Negative

**Objective:** Confirm the server-side validator on `OpenApiConfiguration.headers` (an RFC-7230 token-char regex, read directly in `elitea_sdk/configurations/openapi.py`) rejects an invalid header name — containing a space, a colon, or left blank — on save, surfacing a clear validation error rather than silently saving an invalid name or returning a 500.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.

---

## Test Data

| Field | Value |
|-------|-------|
| Invalid name #1 | `bad header` (space) |
| Invalid name #2 | `bad:header` (colon) |
| Invalid name #3 | *(blank)* |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Add a header row, set name to `bad header`, value to `x`. Attempt to save. | Save is rejected with a clear validation error message (not a 500 or a silent save). |
| 2 | Correct the name; instead set it to `bad:header`, value `x`. Attempt to save. | Save is rejected with a clear validation error. |
| 3 | Correct the name; leave it blank, value `x`. Attempt to save. | Save is rejected with a clear validation error. |
| 4 | Confirm no partial/invalid header was actually persisted after any of the above failed attempts. | Reloading the form shows no invalid header row was saved. |

---

## Expected Final State

None of the three invalid header names is ever persisted; each save attempt surfaces a clear, user-facing validation error.

---

## Pass/Fail Criteria

**Pass:** All three invalid names are rejected on save with a clear error; nothing invalid is persisted.
**Fail:** Any invalid name is silently saved, or the failure produces a 500/unhandled error instead of a clear validation message.
