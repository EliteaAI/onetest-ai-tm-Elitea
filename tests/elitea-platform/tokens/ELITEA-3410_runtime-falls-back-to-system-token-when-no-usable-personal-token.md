---
id: ELITEA-3410
title: "Runtime Falls Back to the System Token When the User Has No Usable Personal Token"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, runtime-fallback]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3410: Runtime Fallback to System Token

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm that when a user has zero personal tokens, or only personal tokens that are all expired, both runtime call sites (MCP injection via `resolve_user_token_state()`, and predict payload via `get_user_token()`) fall back to `ensure_system_token(user_id)` and use that token — instead of the old behavior of failing with "User token not found." This is the core fix this issue exists to deliver: Support Assistant / code node / integrated functions no longer break for users with no PAT.

**Coverage:** AC — "runtime fallback to system token when no usable PAT" (`elitea_core`#435)

## Preconditions

- A user with zero personal tokens (only the auto-provisioned system token exists)
- A second scenario: a user whose only personal token(s) are expired (`expires` in the past)
- Ability to trigger both an MCP-tool-using flow and a predict/chat flow for the test user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As the user with zero personal tokens, trigger an action that requires MCP token injection (e.g. use an MCP-integrated tool in chat). | Action succeeds; internally, `resolve_user_token_state()` found no usable personal token and fell back to `ensure_system_token(user_id)`, using the system token transparently. |
| 2 | As the same user, trigger a predict/chat request (any flow hitting `get_user_token()` in `predict_utils.py`). | Request succeeds using the fallback system token — no "User token not found" error. |
| 3 | Repeat steps 1-2 for the second scenario: a user whose only personal token(s) have `expires` in the past. | Same fallback behavior — expired personal tokens are correctly treated as unusable, system token is used instead. |
| 4 | Confirm the system token itself was never mutated or exposed to the user during this fallback (still hidden per [[ELITEA-3397]]). | System token remains hidden from the user-facing UI/API throughout. |

## Expected Final State

Both call sites successfully complete their operation using the system token whenever the user has no usable personal token, with zero user-visible friction or errors.

## Pass/Fail Criteria

**Pass:**
- Both the MCP-injection and predict-payload paths succeed via system-token fallback in both the zero-tokens and all-expired scenarios

**Fail:**
- Either path still fails/errors when the user has no usable personal token
- The old "User token not found. Please create user_token" error reappears for a covered scenario
