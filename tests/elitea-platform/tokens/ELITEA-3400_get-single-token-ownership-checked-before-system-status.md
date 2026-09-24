---
id: ELITEA-3400
title: "GET Single Token Checks Ownership Before System-Token Status (No Info Leak)"
priority: medium
type: security
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, security]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3400: Ownership Checked Before System-Token Status on `GET /token/<uuid>`

**Module:** Tokens · **Priority:** Medium · **Type:** Security

**Objective:** Confirm `GET /token/<uuid>` checks the caller's ownership of the token BEFORE checking whether it's a system token, so an unauthorized caller can never distinguish "this token belongs to someone else and is a system token" from "this token belongs to someone else and is a personal token" — both must return the same generic 403, never leaking token-type information about another user's token.

**Coverage:** Design detail from `auth`#7 (HTTP API guard table) — ownership-before-system-check ordering

## Preconditions

- Two distinct users, A and B
- User A's `elitea-system` token id known (via `include_system=True`, internal access)
- User A's own personal token id known
- Acting as User B for all requests below

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User B, call `GET /token/<uuid>` using User A's `elitea-system` token id. | `403` — generic "not your token" response, NOT a 404 or any response revealing it's a system token. |
| 2 | As User B, call `GET /token/<uuid>` using User A's personal (non-system) token id. | `403` — same generic response as step 1, indistinguishable in shape/content from step 1. |
| 3 | Compare the two 403 responses from steps 1 and 2 byte-for-byte (status code, body, headers). | Identical — no distinguishing signal about token type leaks through. |
| 4 | As User A (the actual owner), call `GET /token/<uuid>` using their own `elitea-system` token id. | `404` — owner sees "not found" for their own system token (hidden from them too, per [[ELITEA-3397]]), distinct from the 403 an unauthorized caller gets. |
| 5 | As User A, call `GET /token/<uuid>` using their own personal token id. | `200` with the token's details. |

## Expected Final State

Ownership is always checked first: non-owners always get 403 regardless of token type; the owner gets 404 specifically for their own hidden system token, and 200 for their own personal tokens.

## Pass/Fail Criteria

**Pass:**
- Steps 1 and 2 produce identical, generic 403 responses with no system-token signal; step 4 correctly returns 404 (not 403) for the owner's own system token

**Fail:**
- Any response difference between steps 1 and 2 that would let an unauthorized caller infer a token's system/personal status
- Owner's own system-token lookup returns something other than 404 (e.g. leaking existence via a different status/body than the standard "not found" shape)
