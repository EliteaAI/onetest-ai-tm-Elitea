---
id: ELITEA-3031
title: "Empty-State Text Is Shown When No Additional Headers Are Configured"
priority: low
type: ui-validation
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3031: Empty-State Text Is Shown When No Additional Headers Are Configured

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** Low · **Type:** UI Validation

**Objective:** Confirm that with zero additional headers configured, `SecretHeadersInput.jsx` renders the empty-state text "No additional headers configured." and no stray header rows.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create an OpenAPI credential.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | OpenAPI Configuration (any auth method) |
| Additional headers | None configured |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open a new OpenAPI Configuration credential form. | "Additional Secret Headers" section renders. |
| 2 | Inspect the section without adding any header. | Empty-state text "No additional headers configured." is displayed. |
| 3 | Confirm no header name/value/remove inputs are rendered. | No `openapi-secret-header-name-*`/`openapi-secret-header-value-*`/`openapi-secret-header-remove-*` elements are present. |

---

## Expected Final State

The section shows the empty-state message only, with no rows, until a header is explicitly added.

---

## Pass/Fail Criteria

**Pass:** Empty-state text is shown; no rows render.
**Fail:** Empty-state text is missing, incorrect, or a stray/blank row renders with zero headers configured.
