---
id: ELITEA-3399
title: "System Token Cannot Be Deleted by Its Owning User"
priority: high
type: negative
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3399: System Token Cannot Be Deleted

**Module:** Tokens · **Priority:** High · **Type:** Negative

**Objective:** Confirm the `elitea-system` token is protected from deletion at both the HTTP API and RPC layer — a user (or anything acting on their behalf) can never remove their own system token, since doing so would silently break Support Assistant / code node / integrated functions.

**Coverage:** AC — "users cannot delete [the reserved token]"

## Preconditions

- A user whose `elitea-system` token id is known (obtained via `include_system=True` at the RPC/internal level, since it's not visible in the UI/default API — see [[ELITEA-3397]])

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `DELETE /token/<uuid>` with the system token's id. | `403` response, body `{"error": "system token cannot be deleted"}`. |
| 2 | Re-query the user's tokens with `include_system=True`. | System token still exists, unchanged. |
| 3 | At the RPC level, call `delete_token(token_id, allow_system=False)` (the default) directly with the system token id. | Deletion refused (guard enforced at RPC layer, not only HTTP). |
| 4 | Attempt to delete one of the user's own personal (non-system) tokens via the same `DELETE /token/<uuid>` endpoint. | Deletion succeeds normally — only the system token is protected. |

## Expected Final State

The system token remains present and undeletable through every public and internal deletion path exercised; personal token deletion is unaffected.

## Pass/Fail Criteria

**Pass:**
- Every deletion attempt against the system token is refused with the documented 403/error at both HTTP and RPC layers; personal tokens still delete normally

**Fail:**
- System token is deleted through any path (HTTP or RPC)
- Personal token deletion is incorrectly blocked as a side effect
