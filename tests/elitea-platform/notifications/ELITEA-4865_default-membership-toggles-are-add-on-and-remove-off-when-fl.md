---
id: ELITEA-4865
title: "Default membership toggles are add on and remove off when flags were never saved"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4865: Default membership toggles are add on and remove off when flags were never saved

**Module:** admin-portal · **Priority:** critical · **Type:** functional

**Objective:** Verify that with flags never saved the add notification is on and sent, and the remove notification is off and not sent.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- The environment has never saved the Project Membership flags (fresh install or untouched).
- User A is an admin of team project `mariam_test`; User B is logged in to `{{base_url}}` in a second browser profile.
- User B is not a member of `mariam_test`.

---

## Test Data

| Field | Value |
|-------|-------|
| Project | `mariam_test` (team) |
| Role | viewer |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the platform admin open Admin → Features → Notifications | Page loads. |
| 2 | Check "Notify users when added to a team project" | Toggle is **on**. |
| 3 | Check "Notify users when removed from a team project" | Toggle is **off**. |
| 4 | Without saving, as User A invite User B to `mariam_test` as viewer | Invite succeeds. |
| 5 | As User B open the bell popover | An added notification for `mariam_test` is present. |
| 6 | As User A remove User B on Settings → Users | Removal succeeds. |
| 7 | As User B open the bell popover | No removal notification is present. |

---

## Expected Final State

Defaults apply: add notifications are sent, removal notifications are not.

---

## Pass/Fail Criteria

**Pass:**
- Toggles show on/off
- Added notification arrives, removal notification does not

**Fail:**
- Either default is wrong
- Behaviour does not match the defaults
