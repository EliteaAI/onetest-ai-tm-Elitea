---
id: ELITEA-3413
title: "Runtime Fallback Failure Degrades Gracefully Instead of Raising"
priority: medium
type: negative
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, runtime-fallback, resilience]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3413: Fallback Failure Degrades Gracefully

**Module:** Tokens · **Priority:** Medium · **Type:** Negative

**Objective:** Confirm that if `ensure_system_token()` itself fails during the runtime fallback (e.g. DB unavailable, RPC timeout, or the user turns out to be suspended mid-request), both call sites catch the failure via a bare/broad except, log a WARNING (`"Could not ensure system token for user {user_id}"`), and return the old degraded result — rather than raising an unhandled exception up through the chat/predict flow.

**Coverage:** Design detail from `elitea_core`#435 — fallback failures caught, logged, degrade to old `("MISSING", None)`/`None` return values

## Preconditions

- A user with no usable personal token (so the fallback path is actually exercised)
- Ability to make the `ensure_system_token` call fail when invoked from the fallback path (e.g. simulate a suspended user discovered mid-flow, or an RPC timeout/DB error)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Force `ensure_system_token(user_id)` to fail when called from `resolve_user_token_state()`'s fallback branch. | The MCP-injection flow does not crash; it returns the old degraded state `("MISSING", None)`. |
| 2 | Check server logs for this event. | WARNING-level log: "Could not ensure system token for user {user_id}" — no unhandled traceback surfaced as an ERROR/500 to the caller. |
| 3 | Force the same failure from `get_user_token()`'s fallback branch (predict payload path). | Returns `None` gracefully; same WARNING logged. |
| 4 | Confirm the overall user-facing flow (chat message, predict call) still completes in a controlled way (e.g. a normal "couldn't complete this action" style response), not a raw stack trace or hard crash. | Controlled degradation, consistent with pre-existing "no token" handling elsewhere in the flow. |

## Expected Final State

A fallback-provisioning failure is fully contained — logged once as a WARNING, with the caller receiving the same degraded result it always got when no token was available, never an unhandled exception.

## Pass/Fail Criteria

**Pass:**
- Both call sites catch the simulated failure, log the documented WARNING, and return their old degraded value without propagating an exception

**Fail:**
- The failure propagates as an unhandled exception/500 to the end user
- No WARNING is logged, making the failure invisible to operators
