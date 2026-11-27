---
id: ELITEA-5021
title: "Pinned and Recent grouping and pin/unpin move items between groups"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7563, EliteaAI/elitea_issues#7560]
---
# ELITEA-5021: Pinned and Recent grouping and pin/unpin move items between groups

## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has one pinned chat, one unpinned folder with chats inside, and at least two standalone chats

## Test Data

| Group | Expected order |
|-------|----------------|
| Pinned | Pinned folders, then pinned chats |
| Recent | Unpinned folders, then standalone chats, newest first |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` and look at the chat history | Only **Pinned** and **Recent** groups, both expanded, in the order from the Test Data |
| 2 | Collapse **Recent** | All Recent folders and chats are hidden; Pinned is unchanged |
| 3 | Expand **Recent** and pin a standalone chat | The chat moves to **Pinned** |
| 4 | Click the pin icon on that chat | It acts as **Unpin**; the chat returns to **Recent** |
| 5 | Pin the folder, then unpin it | The folder moves to the top of Pinned, then back to the top of Recent, with the same chats inside |

## Expected Final State

Items are in their original groups and folder membership is unchanged.

## Pass/Fail Criteria

**Pass:**
- Grouping, order, collapse and pin/unpin behave as described

**Fail:**
- Date-based groups appear, the order is wrong, or pin/unpin loses, duplicates or moves items out of their folder

## Notes

**Source functional tests:** ELITEA-5016
**Regression rationale:** Pinned/Recent replaces the date groups for every chat list; a break hides or misplaces user chats.
**Selected checkpoints:** Groups and order; collapse; pin and unpin a chat; pin and unpin a folder.
