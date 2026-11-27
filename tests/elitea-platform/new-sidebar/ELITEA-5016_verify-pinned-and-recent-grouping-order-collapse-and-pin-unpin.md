---
id: ELITEA-5016
title: "Verify Pinned and Recent grouping, order, collapse and pin/unpin in the sidebar chat history"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7560, EliteaAI/elitea_issues#7563]
---
# ELITEA-5016: Verify Pinned and Recent grouping, order, collapse and pin/unpin in the sidebar chat history

## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has at least one pinned folder, one pinned chat, one unpinned folder that contains chats, and several standalone chats created at different times

## Test Data

| Group | Expected order |
|-------|----------------|
| Pinned | Pinned folders, then pinned chats |
| Recent | Unpinned folders, then standalone chats, newest first |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Look at the chat history in the sidebar | Only **Pinned** and **Recent** groups are shown, both expanded; Today / Yesterday / This Week / Older are not shown |
| 2 | Check the order inside each group | The order matches the Test Data |
| 3 | Collapse **Pinned**, then expand it and collapse **Recent** | A collapsed group hides all its folders and chats; the other group is not affected |
| 4 | Pin any unpinned standalone chat | The chat moves to **Pinned** |
| 5 | Click the pin icon on that pinned chat | The pin acts as **Unpin**; the chat returns to **Recent** in its newest-first position |
| 6 | Pin the unpinned folder | The folder moves to the top of **Pinned** and its chats stay inside it |
| 7 | Unpin the folder | The folder returns to the top of **Recent** with the same chats inside |

## Expected Final State

All items are in the correct group and folder membership is unchanged.

## Pass/Fail Criteria

**Pass:**
- Only Pinned and Recent groups exist, in the order from the Test Data
- Groups collapse independently; pin/unpin moves items between groups without changing folder membership
- No item is missing or duplicated

**Fail:**
- Date-based groups are still shown, or the order is wrong
- A collapsed group still shows items
- Pinning or unpinning changes folder content, or an item is lost or duplicated
