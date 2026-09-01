---
id: ELITEA-3036
title: "Additional Headers Are Attached to Outbound Requests Even With No Primary Auth (Anonymous)"
priority: medium
type: integration
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, api, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3036: Additional Headers Are Attached to Outbound Requests Even With No Primary Auth (Anonymous)

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** Medium · **Type:** Integration

**Objective:** SDK-level confirmation, directly grounded in `elitea_sdk/tools/openapi/__init__.py` (`_build_additional_headers`, `_merge_primary_headers`) and the SDK's own test `test_additional_headers_work_without_primary_authentication`: with **no** primary auth configured (Authentication Method = Anonymous), additional headers alone must still be attached to outbound requests made through the OpenAPI toolkit.

---

## Preconditions

- An OpenAPI credential with Authentication Method = Anonymous and at least one additional header configured (e.g. `X-Api-Key: abc123`).
- An OpenAPI toolkit built on this credential, added to a chat or otherwise invokable.
- Ability to inspect the outbound HTTP request (e.g. via a request-echoing test endpoint, network capture, or backend logs).

---

## Test Data

| Field | Value |
|-------|-------|
| Auth method | Anonymous |
| Additional header | `X-Api-Key: abc123` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Configure the OpenAPI credential with Anonymous auth and the additional header above. Save. | Save succeeds. |
| 2 | Trigger a tool call through the toolkit (e.g. send a chat message invoking an operation on this toolkit). | Tool call executes. |
| 3 | Inspect the actual outbound request headers. | `X-Api-Key: abc123` is present on the request despite there being no primary `Authorization` header at all. |

---

## Expected Final State

Additional headers function independently of whether a primary auth method is configured.

---

## Pass/Fail Criteria

**Pass:** The additional header is present on the outbound request with Anonymous auth.
**Fail:** The additional header is missing, dropped, or only attached when a primary auth method is also configured.
