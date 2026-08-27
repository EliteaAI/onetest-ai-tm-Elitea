---
id: ELITEA-2831
title: "Admin Portal – Disallowed Projects List Remains Usable and Performant at ~15,000-Project Scale"
priority: high
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-portal, feat:chat, issue:6123, issue:6254, performance]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2831: Admin Portal – Disallowed Projects List Remains Usable and Performant at ~15,000-Project Scale

**Module:** admin-portal · **Priority:** High · **Type:** Functional

**Objective:** Verify the Admin Portal Disallowed Projects picker for follow-up suggestions remains usable when the account/org has a very large number of projects (~15,000): the picker loads within an acceptable time without freezing/crashing the Admin Portal UI, search/filter/pagination work correctly at that scale, edits save successfully without corrupting the list, and per-project flag evaluation at chat-message time stays fast.

---

## Preconditions

- Admin has access to an org/account with approximately 15,000 projects (or an equivalent seeded test environment).
- Follow-up suggestions feature flag is ON globally.

---

## Test Data

| Field | Value |
|-------|-------|
| Project count | ~15,000 projects in the org/account |
| Target project | One specific project to add/remove from the disallow-list during the test |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open the Admin Portal Disallowed Projects picker | Picker opens and loads within an acceptable time; Admin Portal UI does not freeze or crash |
| 2 | Use search/filter within the picker to locate the target project | Search/filter returns correct results promptly at this scale |
| 3 | Use pagination (if present) to page through the project list | Pagination works correctly and consistently at this scale |
| 4 | Add the target project to the disallow-list and save | Save completes successfully without timing out |
| 5 | Reopen the picker and verify the rest of the previously saved disallow-list is intact | No truncation or corruption of the previously saved list |
| 6 | Remove the target project from the disallow-list and save again | Save completes successfully; list updates correctly with no corruption |
| 7 | As a regular user, send a chat message in a project near the "middle" of the 15,000-project org (not the target project) while the disallow-list is at full scale | Feature-flag evaluation for that project completes quickly at message time, with no perceptible chat-side slowdown attributable to disallow-list size |

---

## Expected Final State

The Disallowed Projects picker and the underlying per-project flag evaluation both scale correctly to ~15,000 projects, with no data loss, UI freeze, or runtime slowdown.

---

## Pass/Fail Criteria

**Pass:**
- Picker loads, searches, filters, and paginates correctly at ~15,000-project scale without freezing/crashing.
- Adding/removing a project saves successfully without corrupting or truncating the rest of the list.
- Per-message feature-flag evaluation remains fast regardless of disallow-list size.

**Fail:**
- The picker freezes, crashes, or times out at this scale.
- Search/filter/pagination breaks or becomes unusably slow.
- Saving a single add/remove corrupts or truncates the previously saved list.
- Chat-message-time flag evaluation is measurably slower due to disallow-list size.
