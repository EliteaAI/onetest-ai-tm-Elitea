---
id: ELITEA-3034
title: "Removing a Header Persists After Save/Reload — It Does Not Reappear"
priority: medium
type: functional
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3034: Removing a Header Persists After Save/Reload — It Does Not Reappear

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm removing a header via its remove button (`openapi-secret-header-remove-{index}`) actually deletes it from the persisted configuration, not just from the current form state — it must not reappear after save and reload.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.
- An OpenAPI credential with at least 2 additional headers already saved.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing headers | `X-Trace-Id: t-1`, `X-Tenant: tenant-a` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the credential form with both headers present. | Both rows render. |
| 2 | Click the remove button for `X-Trace-Id`. | Row for `X-Trace-Id` disappears; `X-Tenant` remains. |
| 3 | Save the credential. | Save succeeds. |
| 4 | Reload/reopen the credential form. | Only `X-Tenant` is present; `X-Trace-Id` does not reappear. |

---

## Expected Final State

The removed header is permanently gone from the persisted configuration.

---

## Pass/Fail Criteria

**Pass:** Removed header stays removed after save/reload.
**Fail:** Removed header reappears after reload, indicating the removal wasn't actually persisted.
