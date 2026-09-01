---
id: ELITEA-3037
title: "Additional Headers Combine Correctly With API-Key Auth and With a Delegated OAuth2 Token"
priority: high
type: integration
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, api, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3037: Additional Headers Combine Correctly With API-Key Auth and With a Delegated OAuth2 Token

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Integration

**Objective:** SDK-level confirmation, grounded in `elitea_sdk/tools/openapi/__init__.py`'s `_merge_primary_headers` and the SDK's own tests `test_additional_headers_are_combined_with_api_key_authentication` and `test_additional_headers_are_combined_with_delegated_oauth_token`: both the primary `Authorization` header and the configured extra headers must appear together on the outgoing request — for both an API-key primary auth and a delegated OAuth2 token.

---

## Preconditions

- Two OpenAPI credentials: one with Authentication Method = API Key/Bearer (real key), one with OAuth2 Delegated (Authorization Code) already authorized with a valid token. Both have at least one additional header configured (e.g. `X-Tenant: tenant-a`).
- Toolkits built on each credential, invokable via chat.
- Ability to inspect outbound request headers.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential A | API Key/Bearer + additional header `X-Tenant: tenant-a` |
| Credential B | OAuth2 Delegated (valid token) + additional header `X-Tenant: tenant-a` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Trigger a tool call through the toolkit built on Credential A. | Outbound request carries **both** the real `Authorization: Bearer <key>` header and `X-Tenant: tenant-a`. |
| 2 | Trigger a tool call through the toolkit built on Credential B. | Outbound request carries **both** the real `Authorization: Bearer <oauth-token>` header and `X-Tenant: tenant-a`. |

---

## Expected Final State

Additional headers coexist with the primary auth header in both auth-type scenarios, with neither one displacing the other.

---

## Pass/Fail Criteria

**Pass:** Both the primary auth header and the additional header are present together on both outbound requests.
**Fail:** Either header is missing from either request, or one displaces the other.
