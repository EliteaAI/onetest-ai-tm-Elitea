---
id: ELITEA-0742
title: "Mark all as read applies to full unread dataset"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5119, EliteaAI/elitea_issues#5139]
---
# ELITEA-0742: Mark all as read applies to full unread dataset

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify mark all as read updates entire unread dataset including lazy-loaded items.

**Coverage:**
- Mark all action
- Lazy-loading/Pagination scope validation
- Unread indicator update
- Persistence after reload

## Preconditions

User is logged in
Mark all as read control is available
Unread volume is high enough to trigger lazy loading/pagination

## Test Data

Environment URL: {{base_url}}
Unread dataset size: larger than initial loaded page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open dropdown and note unread indicator | Indicator confirms unread items exist |
| 2 | Without loading all pages click Mark all as read | Indicator clears or updates to zero-state immediately |
| 3 | Refresh page and reopen dropdown | No hidden unread leftovers from same dataset |

## Expected Final State

No hidden unread leftovers from same dataset

## Pass/Fail Criteria

**Pass:**
- All unread items become read, including unloaded rows
- Indicator and persisted state remain correct after reload

**Fail:**
- Only loaded rows are marked read
- Additional unread rows appear after loading more data
