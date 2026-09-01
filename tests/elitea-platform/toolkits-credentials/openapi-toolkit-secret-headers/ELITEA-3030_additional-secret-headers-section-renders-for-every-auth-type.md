---
id: ELITEA-3030
title: "Additional Secret Headers Section Renders for Every OpenAPI Primary Auth Type"
priority: high
type: functional
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, feat:credentials, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3030: Additional Secret Headers Section Renders for Every OpenAPI Primary Auth Type

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Functional

**Objective:** Confirm, as read directly in `SecretHeadersInput.jsx` and its dispatch site `ToolBaseProperty.jsx`, that the "Additional Secret Headers" section (`data-testid="openapi-secret-headers"`) is not gated behind a specific primary auth type — it must render for every OpenAPI Configuration auth method: Anonymous, API Key/Bearer, Basic, Custom header, OAuth2 Client Credentials, and OAuth2 Delegated (Authorization Code).

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit OpenAPI credentials.
- Ability to create an OpenAPI Configuration credential for each primary auth type listed above.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | OpenAPI Configuration |
| Auth types to check | Anonymous, API Key/Bearer, Basic, Custom header, OAuth2 Client Credentials, OAuth2 Delegated |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the OpenAPI Configuration credential form and set Authentication Method = Anonymous. | "Additional Secret Headers" section is visible (`openapi-secret-headers`). |
| 2 | Switch Authentication Method to API Key/Bearer. | Section remains visible, unaffected by the auth-type change. |
| 3 | Switch Authentication Method to Basic. | Section remains visible. |
| 4 | Switch Authentication Method to Custom header. | Section remains visible. |
| 5 | Switch Authentication Method to OAuth2 Client Credentials. | Section remains visible. |
| 6 | Switch Authentication Method to OAuth2 Delegated (Authorization Code). | Section remains visible. |

---

## Expected Final State

The "Additional Secret Headers" section is present and usable regardless of which primary authentication method is selected.

---

## Pass/Fail Criteria

**Pass:** Section renders for all six auth types with no visibility gating.
**Fail:** Section is missing, hidden, or disabled for any one of the auth types.
