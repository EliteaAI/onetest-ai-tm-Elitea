---
id: ELITEA-3039
title: "Header With an Empty Value Is Rejected on Save, Not Silently Partial-Saved"
priority: high
type: negative
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, nfr:validation, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3039: Header With an Empty Value Is Rejected on Save, Not Silently Partial-Saved

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Negative

**Objective:** Confirm `OpenApiConfiguration`'s validator explicitly rejects an empty header value, and that the UI surfaces a clear error on save rather than silently persisting a partial/empty-value header.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.

---

## Test Data

| Field | Value |
|-------|-------|
| Header name | `X-Api-Key` |
| Header value | *(blank)* |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Add a header row, set name to `X-Api-Key`, leave the value field blank. Attempt to save. | Save is rejected with a clear validation error referencing the empty value. |
| 2 | Reload the form. | No header with an empty value was persisted. |

---

## Expected Final State

An empty-value header is never persisted; the save attempt fails with a clear error.

---

## Pass/Fail Criteria

**Pass:** Save is rejected with a clear error; nothing is persisted.
**Fail:** The header is silently saved with an empty value, or the save fails with an unhandled/unclear error.
