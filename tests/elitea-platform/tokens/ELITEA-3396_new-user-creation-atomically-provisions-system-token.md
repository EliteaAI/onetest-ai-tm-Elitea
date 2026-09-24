---
id: ELITEA-3396
title: "New User Creation Atomically Provisions the elitea-system Token"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3396: New User Creation Atomically Provisions the `elitea-system` Token

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm every newly created user account gets exactly one non-expiring token named `elitea-system`, created in the same transaction as the user itself — never a two-step process that could leave a user without a token.

**Coverage:** AC — "Every active user has exactly one platform-managed non-expiring token, held under a reserved name (`elitea-system`)"; AC — "The token is provisioned when a user is created"

## Preconditions

- Ability to create a new user account (admin UI/API) and inspect that user's tokens at the DB/RPC level (`auth_list_tokens` with `include_system=True`, or direct DB read)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new user account. | User created successfully. |
| 2 | Immediately query that user's tokens including system tokens (`include_system=True`). | Exactly one token exists, `name == "elitea-system"`, `expires IS NULL`. |
| 3 | Confirm no additional personal tokens were auto-created. | Only the one system token exists; user's visible token list (default, `include_system=False`) is empty. |
| 4 | Repeat steps 1-3 for several new users in quick succession. | Each user gets exactly one system token; no cross-contamination (User B never gets User A's token). |

## Expected Final State

Every new user has exactly one `elitea-system` token, non-expiring, created atomically with the account.

## Pass/Fail Criteria

**Pass:**
- New user has exactly one `elitea-system` token with `expires IS NULL` immediately after creation

**Fail:**
- User created without a system token (requiring a later login to self-heal it)
- More than one system-named token exists for a single user
- Token has a non-null expiry
