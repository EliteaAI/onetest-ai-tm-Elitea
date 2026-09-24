---
id: ELITEA-3404
title: "Reinstated User Gets a System Token Minted on Next Login"
priority: medium
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, suspension]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3404: Reinstated User Gets a System Token on Next Login

**Module:** Tokens · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that once a suspended user (who has no system token yet — see [[ELITEA-3403]]) is reinstated, their normal access is restored and the next login self-heals a system token for them, exactly like any other pre-existing user without one.

**Coverage:** Design detail from `auth_core`#12 — reinstatement restores access and mints a token on next login

## Preconditions

- A user account that was suspended and has no `elitea-system` token
- Ability to reinstate (un-suspend) the account via admin action

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the suspended user has no `elitea-system` token (per [[ELITEA-3403]]). | Confirmed absent. |
| 2 | Reinstate the user's account (remove suspension). | Account is active again. |
| 3 | Log in as the reinstated user. | Login succeeds normally. |
| 4 | Query the user's tokens with `include_system=True`. | Exactly one `elitea-system` token now exists, `expires IS NULL`. |

## Expected Final State

Reinstatement restores full access, and the standard login self-heal path provisions the missing system token exactly as it would for any never-suspended user.

## Pass/Fail Criteria

**Pass:**
- Reinstated user logs in successfully and receives a system token on that first post-reinstatement login

**Fail:**
- Login fails after reinstatement
- No system token is created despite a successful login
