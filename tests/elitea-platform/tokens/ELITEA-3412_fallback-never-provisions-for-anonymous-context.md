---
id: ELITEA-3412
title: "System Token Fallback Never Triggers in an Anonymous (No user_id) Context"
priority: high
type: security
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, runtime-fallback, security]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3412: Fallback Never Provisions Without a `user_id`

**Module:** Tokens · **Priority:** High · **Type:** Security

**Objective:** Confirm both runtime fallback call sites guard `user_id is None` FIRST, before any token lookup — because `list_tokens(None)` would otherwise return every token in the entire table, and provisioning/using a token in an anonymous context would be a serious cross-account leak. Anonymous or unauthenticated contexts must fail closed (old `("MISSING", None)` / `None` behavior), never silently pick up an arbitrary token.

**Coverage:** Design detail from `elitea_core`#435 — `if user_id is None` guard precedes the token-lookup loop at both call sites

## Preconditions

- Ability to trigger the MCP-injection (`resolve_user_token_state()`) and predict-payload (`get_user_token()`) code paths in a context where `user_id` is `None` (e.g. an anonymous/unauthenticated request, or a code path that legitimately has no associated user)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger `resolve_user_token_state()` (or the flow that calls it) with `user_id=None`. | Returns the old degraded state (`("MISSING", None)`) immediately — no `list_tokens` call is made, no token of any kind (personal or system) is returned. |
| 2 | Trigger `get_user_token()` (or the flow that calls it) with `user_id=None`. | Returns `None` immediately — same guard-first behavior, no fallback attempted. |
| 3 | Confirm via logs/tracing that `list_tokens` was never invoked with `user_id=None` in either case. | No call made — the `is None` check short-circuits before any DB query. |
| 4 | Confirm no `ensure_system_token` call was made either. | No provisioning attempt occurs for an anonymous context. |

## Expected Final State

An anonymous/no-user_id context always fails closed, exactly as it did before this feature — the new fallback logic introduces zero new exposure for unauthenticated contexts.

## Pass/Fail Criteria

**Pass:**
- Both call sites return their documented "missing" result immediately for `user_id=None`, with no `list_tokens`/`ensure_system_token` calls made

**Fail:**
- Any token (personal or system, belonging to any user) is returned or used when `user_id` is `None`
- `list_tokens(None)` is actually invoked, returning the full unfiltered token table into the fallback logic
