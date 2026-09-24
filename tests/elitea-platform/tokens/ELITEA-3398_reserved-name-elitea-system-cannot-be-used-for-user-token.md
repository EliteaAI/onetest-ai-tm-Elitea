---
id: ELITEA-3398
title: "Reserved Name elitea-system Cannot Be Used for a User-Created Token"
priority: high
type: negative
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3398: Reserved Name `elitea-system` Cannot Be Used for a User-Created Token

**Module:** Tokens · **Priority:** High · **Type:** Negative

**Objective:** Confirm a user cannot create a personal token literally named `elitea-system` — the name check is an exact, case-sensitive match, so verify both the blocked exact case and that near-miss casing is treated as a genuinely different (allowed) name.

**Coverage:** AC — "users cannot ... create a token under the reserved name"

## Test Data

| Name attempted | Expected |
|-----------------|----------|
| `elitea-system` | Rejected — exact reserved match |
| `Elitea-System` | Allowed — different string, not the reserved name (case-sensitive match) |
| `elitea-system-conflict-123` | Allowed — not the reserved name itself |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Attempt to create a token named exactly `elitea-system` via the UI. | Creation blocked with an inline error. |
| 2 | Attempt the same via `POST /token` directly with `name: "elitea-system"`. | `400` response, body `{"error": "Name \"elitea-system\" is reserved"}`. |
| 3 | Attempt to create a token named `Elitea-System` (different casing). | Creation succeeds — this is a distinct, permitted name. |
| 4 | Attempt to create a token named `elitea-system-conflict-123`. | Creation succeeds. |

## Expected Final State

Only the exact string `elitea-system` is blocked; any other casing or variant is a normal, permitted user token name.

## Pass/Fail Criteria

**Pass:**
- Exact-match `elitea-system` is rejected with the documented 400/error; casing variants and near-miss strings succeed normally

**Fail:**
- Exact-match creation succeeds (reserved name bypassed)
- A differently-cased or near-miss name is incorrectly blocked (over-broad matching)
