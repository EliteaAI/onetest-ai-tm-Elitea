---
id: ELITEA-3401
title: "Login Self-Heals a Missing System Token for Pre-Existing Users"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3401: Login Self-Heals a Missing System Token

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm that a pre-existing user who does not yet have an `elitea-system` token (e.g. created before this feature shipped, and not yet covered by the backfill migration) automatically gets one minted the next time they log in — without any visible delay, error, or friction in the login flow.

**Coverage:** AC — "self-heals missing token on login" (`auth_init`#2)

## Preconditions

- A user account exists in the DB with no `elitea-system` token (simulate by deleting the row directly, or use a pre-migration snapshot/test user)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm via `include_system=True` that the test user currently has zero tokens named `elitea-system`. | Confirmed absent. |
| 2 | Log in as that user normally (standard credentials flow). | Login succeeds with no visible error, delay, or extra step. |
| 3 | Immediately after login, query the user's tokens with `include_system=True`. | Exactly one `elitea-system` token now exists, `expires IS NULL`. |
| 4 | Log out and log in again as the same user. | Login succeeds; no duplicate system token is created (still exactly one). |

## Expected Final State

The user ends up with exactly one system token after their first post-gap login, with no user-visible impact on the login experience.

## Pass/Fail Criteria

**Pass:**
- Missing system token is created transparently on login; a second login does not create a duplicate

**Fail:**
- Login fails, errors, or is visibly delayed while healing the token
- No token is created after login
- A duplicate system token is created on a subsequent login
