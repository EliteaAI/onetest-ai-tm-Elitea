---
id: ELITEA-3044
title: "Primary-Auth Override Protection Is Genuinely Case-Insensitive on the Header Name, Not Just an Exact-String Match"
priority: high
type: security
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, nfr:security, api, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3044: Primary-Auth Override Protection Is Genuinely Case-Insensitive on the Header Name, Not Just an Exact-String Match

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Security

**Objective:** SDK-level follow-up to [[ELITEA-3043]]: confirm the override protection in `_merge_primary_headers()` is genuinely case-insensitive on the header **name**, not an exact-string match that would let a casing variant slip through. Try `AUTHORIZATION`, `authorization`, and `Authorization` as three separate spoofing attempts (one per test credential) and confirm all three are neutralized identically.

---

## Preconditions

- An OpenAPI credential with Authentication Method = API Key/Bearer configured with a real, known key.
- Ability to inspect the actual outbound HTTP request per tool call.

---

## Test Data

| Field | Value |
|-------|-------|
| Primary auth | API Key/Bearer, real key `real-bearer-token` |
| Spoof attempt A | Additional header name `AUTHORIZATION`, value `attacker-a` |
| Spoof attempt B | Additional header name `authorization`, value `attacker-b` |
| Spoof attempt C | Additional header name `Authorization`, value `attacker-c` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Configure the credential with additional header `AUTHORIZATION` = `attacker-a`. Save and trigger a tool call. | Outbound `Authorization` header carries `Bearer real-bearer-token`, not `attacker-a`. |
| 2 | Reconfigure with additional header `authorization` = `attacker-b`. Save and trigger a tool call. | Outbound `Authorization` header carries `Bearer real-bearer-token`, not `attacker-b`. |
| 3 | Reconfigure with additional header `Authorization` = `attacker-c`. Save and trigger a tool call. | Outbound `Authorization` header carries `Bearer real-bearer-token`, not `attacker-c`. |

---

## Expected Final State

All three casing variants of `Authorization` are neutralized identically — the override protection is not case-sensitive in any way that could be bypassed.

---

## Pass/Fail Criteria

**Pass:** All three casing variants are neutralized identically; the real Bearer token is always what's sent.
**Fail:** Any one casing variant (e.g. all-caps `AUTHORIZATION`) succeeds in overriding the real header where the exact-case variant did not.
