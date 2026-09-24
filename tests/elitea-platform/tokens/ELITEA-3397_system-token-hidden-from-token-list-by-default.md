---
id: ELITEA-3397
title: "System Token Is Hidden From the User's Token List (UI and API) by Default"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3397: System Token Hidden From the Token List by Default

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm the `elitea-system` token never appears in the user-facing Personal Access Tokens UI, nor in the default `GET /token` API listing — it's only visible via the internal `include_system=True` path.

**Coverage:** AC — "The token is hidden from the user's token management interface"

## Preconditions

- A user whose only token is the auto-provisioned `elitea-system` token (no personal tokens created yet)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as that user and open the Personal Access Tokens management page. | Page shows an empty list (no tokens), despite the system token existing in the DB. |
| 2 | Call `GET /token` directly (no special params). | Returns `[]`. |
| 3 | Create one personal token via the UI. | Personal token appears in both UI and `GET /token`; the system token still does not. |
| 4 | Query the same user's tokens with `include_system=True` at the RPC/internal level (not via the public API). | Both the personal token and the `elitea-system` token are returned. |

## Expected Final State

The public-facing token list (UI and default API) only ever shows user-created tokens; the system token is visible exclusively through the internal `include_system=True` path.

## Pass/Fail Criteria

**Pass:**
- System token absent from UI and default `GET /token` response in every case, present only via `include_system=True`

**Fail:**
- System token appears anywhere in the user-facing UI or default API listing
