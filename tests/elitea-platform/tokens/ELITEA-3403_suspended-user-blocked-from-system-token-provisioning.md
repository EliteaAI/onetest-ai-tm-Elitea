---
id: ELITEA-3403
title: "Suspended Users Are Blocked From System Token Provisioning and Authentication"
priority: high
type: negative
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, suspension]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3403: Suspended Users Are Blocked From System Token Provisioning

**Module:** Tokens · **Priority:** High · **Type:** Negative

**Objective:** Confirm a suspended user's account cannot have an `elitea-system` token minted or used for authentication — `ensure_system_token()` and both bearer/basic-auth entry points raise `ValueError: User is suspended` (or the user-id-specific variant) rather than silently succeeding or provisioning a token for a suspended account.

**Coverage:** Design detail from `auth_core`#12 / `auth`#7 — suspension guards on `ensure_system_token`, `handle_bearer_token`

## Preconditions

- A user account that is administratively suspended
- Access to call `ensure_system_token(user_id)` directly (internal/RPC level) and to attempt normal login for the suspended user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Attempt to log in as the suspended user via the normal UI login flow. | Login is rejected/blocked (suspension enforced as before — no regression from this feature). |
| 2 | At the RPC/internal level, call `ensure_system_token(user_id)` directly for the suspended user's id. | Raises `ValueError: User is suspended: {user_id}` — no token is created. |
| 3 | Attempt bearer-token authentication using any existing token belonging to the suspended user (if one exists from before suspension). | `handle_bearer_token()` raises `ValueError: User is suspended` — access denied. |
| 4 | Repeat step 3 using basic-auth credentials for the suspended user. | Same suspension error — both auth entry points are covered. |
| 5 | Confirm no `elitea-system` token was created for the suspended user as a side effect of any of the above attempts. | `include_system=True` query shows no system token exists for this user (unless one predated suspension). |

## Expected Final State

A suspended user cannot authenticate through any path, and no system token gets provisioned for them while suspended.

## Pass/Fail Criteria

**Pass:**
- All four access attempts (login, ensure_system_token, bearer auth, basic auth) are rejected with the suspension error; no token is created

**Fail:**
- Any access path succeeds for the suspended user
- A system token is silently created for a suspended user
