---
id: ELITEA-3033
title: "Header Name Round-Trips Exactly on Save/Reload; Value Is Masked, Consistent With Other Secret Fields"
priority: high
type: functional
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, feat:credentials, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3033: Header Name Round-Trips Exactly on Save/Reload; Value Is Masked, Consistent With Other Secret Fields

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Functional

**Objective:** Confirm a header's name and value persist correctly through a save/reload cycle: the name round-trips exactly as entered, and the value is masked/hidden on reload via `SecretManagementInput`'s secret-field behavior — the same behavior already relied upon for other secret fields in this form (API key, client secret).

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.

---

## Test Data

| Field | Value |
|-------|-------|
| Header name | `X-Api-Key` |
| Header value | `abc123` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the OpenAPI credential form, click **+ Add header**, set the name to `X-Api-Key` and the value to `abc123`. | Row accepts both values. |
| 2 | Save the credential. | Save succeeds with no error. |
| 3 | Reload/reopen the credential form. | The header row still exists; the name field shows exactly `X-Api-Key`. |
| 4 | Inspect the value field. | The value is masked/hidden (not shown in plaintext), matching the masking behavior of the API key/client secret fields elsewhere in the same form. |

---

## Expected Final State

The header name persists exactly; the value persists but is never shown in plaintext after reload.

---

## Pass/Fail Criteria

**Pass:** Name round-trips exactly; value is masked on reload, consistent with other secret fields.
**Fail:** Name is altered/truncated on reload, or the value is shown in plaintext.
