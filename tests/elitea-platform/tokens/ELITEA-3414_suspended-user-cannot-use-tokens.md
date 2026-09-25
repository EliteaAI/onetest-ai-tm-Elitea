---
id: ELITEA-3414
title: "Suspended User Cannot Use Their Tokens"
priority: low
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, suspension]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3414: Suspended User Cannot Use Their Tokens

**Module:** Tokens · **Priority:** Low · **Type:** Functional

**Objective:** Confirm that once a user is suspended, they can no longer authenticate or use the platform via their tokens (personal or system) — access is blocked while suspended.

**Coverage:** AC — suspension is respected, not bypassed

## Preconditions

- An active user with at least one valid personal token (or relying on the system token)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the user can authenticate/use the platform normally (e.g. log in, or call an API using their token). | Works as expected. |
| 2 | Suspend the user's account. | Account is suspended. |
| 3 | Attempt to log in as the user, or use their existing token to call the API. | Access is refused (login fails / token calls are rejected) for the suspended user. |

## Expected Final State

A suspended user cannot use the platform through any token-based access path while suspended.

## Pass/Fail Criteria

**Pass:**
- Suspended user is blocked from logging in and from using their token(s)

**Fail:**
- Suspended user is still able to log in or use their token(s) to access the platform
