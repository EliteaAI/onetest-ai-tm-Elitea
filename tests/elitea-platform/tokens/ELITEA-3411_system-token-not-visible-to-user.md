---
id: ELITEA-3411
title: "System Token Is Not Visible to the User"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3411: System Token Is Not Visible to the User

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm the auto-provisioned `elitea-system` token never appears anywhere a user can see — the Personal Access Tokens page in the UI, and the default token-listing API — even though it exists and is actively usable behind the scenes.

**Coverage:** AC — "The token is hidden from the user's token management interface"

## Preconditions

- A user account (any state — new or pre-existing), which has an `elitea-system` token provisioned

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as the user and open the Personal Access Tokens management page. | The system token does not appear in the list, regardless of how many other personal tokens the user has. |
| 2 | Call the token-listing API endpoint directly with default parameters (no special "include system" flag). | Response does not include the system token. |
| 3 | Create a new personal token and view the list again (UI and API). | The new personal token appears; the system token still does not. |

## Expected Final State

The system token remains completely invisible through every user-facing surface, regardless of how many personal tokens exist.

## Pass/Fail Criteria

**Pass:**
- System token is absent from the UI and default API listing in every scenario tried

**Fail:**
- System token appears in the UI or the default API listing under any condition
