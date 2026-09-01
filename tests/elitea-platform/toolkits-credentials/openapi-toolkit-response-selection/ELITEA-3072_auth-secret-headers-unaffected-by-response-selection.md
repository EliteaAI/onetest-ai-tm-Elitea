---
id: ELITEA-3072
title: "Auth/Secret Headers Are Unaffected by response_search/response_limit Usage"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, issue:6002, api, security]
requirements: [EliteaAI/elitea_issues#6105, EliteaAI/elitea_issues#6002]
---

# ELITEA-3072: Auth/Secret Headers Are Unaffected by Response Selection Usage

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm that using `response_search`/`response_limit` on an OpenAPI operation has no effect on the toolkit's handling of authentication/secret headers (as introduced/hardened for [[ELITEA-3030]]–[[ELITEA-3046]] under #6002) — headers are attached identically whether or not selection args are supplied, and selection-arg processing never exposes, logs, or alters header/secret values.

---

## Preconditions

- A credential/toolkit configured with a secret/auth header (per the #6002 additional-secret-headers feature).
- An OpenAPI operation on that toolkit reachable with and without `response_search`/`response_limit`.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential | one configured with an additional secret header (per #6002) |
| Calls | (a) operation with no selection args, (b) same operation with `response_search`+`response_limit` set |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the operation with no selection args. | Request succeeds; secret header sent correctly (baseline, per #6002 behavior). |
| 2 | Call the same operation with `response_search`/`response_limit` set. | Request succeeds; secret header sent identically to step 1. |
| 3 | Inspect the `_elitea_response_selection` metadata and returned content for any leakage of header/secret values. | No header/secret values appear anywhere in the response metadata or filtered content. |

---

## Expected Final State

Response-selection processing is fully orthogonal to auth/secret header handling — no interaction, no leakage.

---

## Pass/Fail Criteria

**Pass:** Identical header behavior with/without selection args; no secret values ever surfaced in selection output.
**Fail:** Header behavior differs when selection args are used, or any secret value appears in the response/metadata.
