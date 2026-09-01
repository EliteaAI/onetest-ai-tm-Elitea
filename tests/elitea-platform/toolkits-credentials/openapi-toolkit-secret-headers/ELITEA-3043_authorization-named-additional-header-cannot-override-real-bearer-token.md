---
id: ELITEA-3043
title: "An Additional Header Literally Named Authorization (Any Casing) Cannot Override the Real Bearer Token"
priority: critical
type: security
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, feat:credentials, int:openapi, issue:6002, nfr:security, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3043: An Additional Header Literally Named Authorization (Any Casing) Cannot Override the Real Bearer Token

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** Critical · **Type:** Security

**Objective:** Confirm the highest-value security guarantee of this feature, directly read in `_merge_primary_headers()` (`elitea_sdk/tools/openapi/__init__.py`): the function deletes any existing header matching the primary auth header's name **case-insensitively** before inserting the real primary header. Configure primary auth as API Key/Bearer with a real key, and add an additional header literally named `Authorization` (in any casing: `Authorization`, `AUTHORIZATION`, `authorization`) with an attacker-chosen value. On tool call, confirm the **real** Bearer token is what's actually sent — the attacker-supplied value is silently discarded, never merged. Note for test design: the UI (`SecretHeadersInput.jsx`) has **no client-side block** on naming a header `Authorization` — the form will happily let you save it. The protection lives at the SDK merge layer, not the form; this is intentional per the code, so the UI's lack of a warning is not itself a defect.

---

## Preconditions

- An OpenAPI credential with Authentication Method = API Key/Bearer configured with a real, known key.
- An OpenAPI toolkit built on this credential, invokable via chat.
- Ability to inspect the actual outbound HTTP request sent by the tool call (e.g. a request-echoing test endpoint, network capture, or backend logs).

---

## Test Data

| Field | Value |
|-------|-------|
| Primary auth | API Key/Bearer, real key `real-bearer-token` |
| Additional header (spoof attempt) | Name `Authorization`, value `attacker-value` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Configure the credential with the real Bearer key above. | Primary auth saved. |
| 2 | Add an additional header named `Authorization` with value `attacker-value`. Save. | The UI allows this to be saved without any client-side block or warning (confirm this is the actual behavior, not assumed). |
| 3 | Trigger a tool call through the toolkit built on this credential. | Tool call executes. |
| 4 | Inspect the actual `Authorization` header on the outbound request. | The header's value is the real `Bearer real-bearer-token` — **not** `attacker-value`. The attacker-supplied value never reaches the outbound request. |

---

## Expected Final State

The spoofed `Authorization` header configured as an "additional header" is always silently discarded in favor of the real primary auth header, regardless of the UI having allowed it to be saved.

---

## Pass/Fail Criteria

**Pass:** The outbound request's `Authorization` header carries the real Bearer token; the attacker-supplied additional-header value never appears on the wire.
**Fail:** The attacker-supplied value from the additional header appears on the outbound request instead of (or alongside, as a second conflicting header) the real Bearer token.
