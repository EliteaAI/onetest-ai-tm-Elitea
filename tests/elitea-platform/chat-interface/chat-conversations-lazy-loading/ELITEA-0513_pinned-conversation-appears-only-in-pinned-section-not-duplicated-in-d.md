---
id: ELITEA-0513
title: "Pinned Conversation Appears Only in Pinned Section — Not Duplicated in Date Groups After Reload"
priority: critical
type: functional
module: chat-conversations-lazy-loading
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5008]
---
# ELITEA-0513: Pinned Conversation Appears Only in Pinned Section — Not Duplicated in Date Groups After Reload

**Module:** Chat Conversations Lazy Loading · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pinned conversation appears only in the Pinned section and is excluded from all regular date group sections (Today, This Week, Older) — with no duplication after page reload.

**Coverage:**
- Pinned conversation is visible in the Pinned section
- Pinned conversation does NOT appear in Today / This Week / Older groups
- Behavior is consistent after page reload (the confirmed regression trigger)

## Preconditions

- Logged in to {{base_url}}
- At least one existing conversation available to pin

## Test Data

- Any conversation created today, this week, or older that can be pinned
- Browser: any supported browser with hard-reload capability (F5 / Ctrl+Shift+R)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Identify a conversation in any date group (Today, This Week, or Older). Right-click or use its context menu and select Pin. | The conversation moves to the Pinned section at the top. It is no longer visible in its original date group. |
| 2 | Without reloading, check all date group sections (Today, This Week, Older) for the pinned conversation. | The pinned conversation does not appear in any regular date group — only in Pinned. |
| 3 | Reload the page (F5 or browser refresh). | Page reloads. The conversation is still visible in the Pinned section. |
| 4 | Check all date group sections (Today, This Week, Older) again after reload. | The pinned conversation is NOT present in any regular date group. No duplication. Only one entry exists — in Pinned. |

## Expected Final State

The pinned conversation is NOT present in any regular date group. No duplication. Only one entry exists — in Pinned.

## Pass/Fail Criteria

**Pass:**
- Pinned conversation appears only in the Pinned section
- No duplicate of the pinned conversation exists in Today / This Week / Older after reload

**Fail:**
- Pinned conversation appears both in the Pinned section and in any regular date group
- Duplicate is visible either before or after page reload
