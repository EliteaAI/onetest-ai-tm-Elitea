---
id: ELITEA-3411
title: "Runtime Always Prefers the User's Own Personal Token Over the System Token"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, runtime-fallback]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3411: Runtime Prefers Personal Token Over System Token

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm the system token is strictly a last-resort fallback — a user who has at least one valid (non-expired) personal token always gets that personal token used at runtime, never the system token, at both the MCP-injection and predict-payload call sites.

**Coverage:** Design detail from `elitea_core`#435 — loop finds first token with `expires IS None or expires > now` and returns it; system token never touched if a usable personal token exists

## Preconditions

- A user with at least one valid (non-expired, or `expires IS NULL`) personal token, in addition to their auto-provisioned system token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As this user, trigger an MCP-tool-using flow. | The user's personal token is used for MCP injection — confirm via logs/traffic inspection that the token id used matches the personal token, not the system token. |
| 2 | As this user, trigger a predict/chat flow. | Same confirmation for `get_user_token()` — personal token id used, not the system token's. |
| 3 | Give the user two valid personal tokens (both non-expired). | Either is acceptable per "first token found" semantics — but critically, still never the system token. |
| 4 | Expire the user's only valid personal token, then repeat step 1. | Now falls back to the system token (per [[ELITEA-3410]]) — confirms the preference is dynamic, not cached incorrectly from a prior lookup. |

## Expected Final State

The system token is only ever used when zero valid personal tokens exist; its presence never overrides an otherwise-usable personal token.

## Pass/Fail Criteria

**Pass:**
- Personal token is used in every case where one is valid; system token is used only once the personal token expires

**Fail:**
- The system token is used even though the user has a valid personal token available
