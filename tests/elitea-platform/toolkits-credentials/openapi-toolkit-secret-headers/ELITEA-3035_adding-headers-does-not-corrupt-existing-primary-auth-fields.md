---
id: ELITEA-3035
title: "Adding Additional Headers Does Not Corrupt Existing Primary Auth Fields"
priority: high
type: regression
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, feat:credentials, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3035: Adding Additional Headers Does Not Corrupt Existing Primary Auth Fields

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Regression

**Objective:** Confirm that adding and saving additional secret headers alongside a fully-configured primary auth method does not clear or corrupt the existing primary auth fields (`api_key`, `client_id`, `client_secret`, `custom_header_name`, etc.) — a straightforward no-regression check on a form that now has an extra, independently-managed section.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.
- An OpenAPI credential already configured and saved with one of: API Key/Bearer, Basic, Custom header, or OAuth2 Client Credentials.

---

## Test Data

| Field | Value |
|-------|-------|
| Primary auth (pick one) | API Key/Bearer with a real key, or Custom header with a real header name/value |
| Additional headers to add | `X-Api-Key: abc123`, `X-Tenant: tenant-a` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the existing OpenAPI credential with primary auth already configured. | Primary auth fields show their existing values (masked as applicable). |
| 2 | Add 2 additional headers via **+ Add header**. | Both rows added successfully. |
| 3 | Save the credential. | Save succeeds. |
| 4 | Reload/reopen the credential form. | Primary auth fields are unchanged from before step 2 — no field was cleared, blanked, or altered. |
| 5 | Confirm the additional headers also persisted correctly. | Both headers are present as configured in step 2. |

---

## Expected Final State

Primary auth configuration and additional headers coexist correctly with no cross-contamination.

---

## Pass/Fail Criteria

**Pass:** Primary auth fields are unaffected; additional headers persist correctly alongside them.
**Fail:** Any primary auth field is cleared, blanked, or altered as a side effect of adding/saving additional headers.
