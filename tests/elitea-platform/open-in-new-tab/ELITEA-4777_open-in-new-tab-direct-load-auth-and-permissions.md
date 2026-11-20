---
id: ELITEA-4777
title: "Open in new tab: Direct load, auth and permissions"
priority: medium
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, permissions, auth, direct-url, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4777: Open in new tab: Direct load, auth and permissions

**Module:** open-in-new-tab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that links opened in a new tab load directly, require login when the session is absent, and respect existing permissions.

**Coverage:**
- Direct load and refresh
- Logged-out access redirects to login, then to the destination
- Restricted user cannot access restricted entities/projects

## Preconditions
- User A: full access to Project A.
- User B: no access to Project A (or to a specific entity).
- Project A has at least one Agent.

## Test Data
- Agent link: `/app/<projectA-id>/...` (copied from the agent card)

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open the agent in a new tab and refresh it | Page loads directly and fully, with no dependency on the original tab |
| 2 | Copy the agent link (right-click → Copy link address) | Link is copied |
| 3 | Log out (or use a private window) and paste the link | Redirected to login |
| 4 | Log in as User A | Correct agent opens after login |
| 5 | Log in as User B and open the copied link | Standard access-restriction behaviour is shown; no agent data is exposed |

## Expected Final State
Direct loading works and permissions are enforced in new tabs exactly as before.

## Pass/Fail Criteria
- **Pass:** Direct load works, login redirect returns to the destination, and restricted users see no data.
- **Fail:** Blank/error page on direct load, redirect loses the destination, or restricted data is shown.
