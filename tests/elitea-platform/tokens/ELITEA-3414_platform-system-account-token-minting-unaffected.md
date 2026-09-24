---
id: ELITEA-3414
title: "Platform's Own SystemToken.create() Account Minting Is Unaffected by the New Hidden System Token"
priority: medium
type: regression
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, regression]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3414: Platform Account Token Minting (`SystemToken.create()`) Is Unaffected

**Module:** Tokens · **Priority:** Medium · **Type:** Regression

**Objective:** Confirm the platform's own pre-existing system-account token minting flow (`SystemToken.create()`, unrelated in name only to the new `elitea-system` feature) continues minting/reusing its `api`-named token exactly as before — it must never see or opt into the new hidden per-user system token, since it deliberately calls `list_tokens(system_user_id)` without `include_system=True`.

**Coverage:** Regression guarantee from `projects`#13 — `test_does_not_opt_into_seeing_system_tokens` mutation test proves `include_system=True` is never passed by this flow

## Preconditions

- Access to trigger the platform's internal system-account token flow (whatever internal process calls `SystemToken.create()`)
- The platform's system account should also now have its own auto-provisioned `elitea-system` token (since it's a user account too)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the platform's system account has both: an `api`-named token (from `SystemToken.create()`, pre-existing behavior) and an `elitea-system` token (new, auto-provisioned per [[ELITEA-3396]]). | Both tokens coexist for this account. |
| 2 | Trigger the flow that calls `SystemToken.create()` again (reuse case). | Returns/reuses the existing `api`-named token — unaffected by the presence of the `elitea-system` token. |
| 3 | Delete the `api`-named token and trigger `SystemToken.create()` again (recreate case). | A new `api`-named token is minted, exactly as before this feature existed. |
| 4 | Confirm at no point does this flow's `list_tokens` call include `include_system=True`. | Consistent with the `test_does_not_opt_into_seeing_system_tokens` guarantee — this flow is structurally blind to the system token. |

## Expected Final State

`SystemToken.create()` behaves identically to its pre-#5262 behavior in every scenario; the new hidden token is invisible to it.

## Pass/Fail Criteria

**Pass:**
- Token minting/reuse behavior for the platform's own account is unchanged in both the reuse and recreate scenarios

**Fail:**
- `SystemToken.create()` returns, reuses, or is confused by the `elitea-system` token
- The flow starts passing `include_system=True` (scope creep regression)
