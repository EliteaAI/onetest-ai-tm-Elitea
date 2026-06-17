---
id: ELITEA-0514
title: "Conversation Lazy Loading Works for Conversations Inside Folders"
priority: high
type: functional
module: chat-conversations-lazy-loading
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4834]
---
# ELITEA-0514: Conversation Lazy Loading Works for Conversations Inside Folders

**Module:** Chat Conversations Lazy Loading · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations organized inside folders are loaded correctly via lazy loading — folder structure is preserved and conversations inside folders are fetchable by scrolling, not skipped or lost.

**Coverage:**
- Folders are visible in the sidebar alongside ungrouped conversations
- Expanding a folder with many conversations triggers batch loading inside the folder
- Conversations inside folders appear correctly without duplicates or missing items

## Preconditions

- Logged in to {{base_url}}
- A project where at least one folder exists containing 20+ conversations
- Additional ungrouped conversations also present in the sidebar
- DevTools → Network → Filter: `conversations`

## Test Data

- Folder name: any folder with 20+ conversations inside
- Ungrouped conversations: at least 10 outside any folder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Observe the sidebar. | Folders are visible in the sidebar. Ungrouped conversations also appear. No errors. |
| 2 | Expand a folder that contains 20+ conversations. | Conversations inside the folder load correctly. If the folder has more than the batch limit, scrolling inside it triggers additional batch requests with incremented `offset`. |
| 3 | Scroll through the conversations inside the folder until all are loaded. | All conversations inside the folder are displayed. No conversations are missing. Folder structure is preserved. |
| 4 | Scroll through ungrouped conversations in the sidebar to verify lazy loading still works outside folders. | Ungrouped conversations continue to load in batches normally. Folder and non-folder lazy loading do not interfere with each other. |

## Expected Final State

Ungrouped conversations continue to load in batches normally. Folder and non-folder lazy loading do not interfere with each other.

## Pass/Fail Criteria

**Pass:**
- Conversations inside folders load correctly via lazy loading
- Folder structure is preserved in the sidebar
- Ungrouped conversation lazy loading is unaffected

**Fail:**
- Conversations inside folders are missing or not displayed
- Expanding a folder causes an error or blank state
- Folder and non-folder loading interfere with each other
