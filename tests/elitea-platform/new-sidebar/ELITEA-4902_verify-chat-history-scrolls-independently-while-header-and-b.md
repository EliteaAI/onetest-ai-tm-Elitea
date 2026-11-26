---
id: ELITEA-4902
title: "Verify chat history scrolls independently while header and bottom row stay visible"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4902: Verify chat history scrolls independently while header and bottom row stay visible


## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has enough chats to overflow the sidebar (30+ chats)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Viewport | 1366 × 768 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` with the sidebar expanded | The Chats history overflows the visible area |
| 2 | Scroll down inside the Chats history | Only the history scrolls. The logo/bell, project selector, + New chat, Artifacts and Explore stay in place |
| 3 | Scroll to the bottom of the history | The bottom row (Settings, Help, Support Assistant) stays visible and isn't pushed out of view |
| 4 | Scroll the main page content | The sidebar doesn't scroll |

## Expected Final State

The history scrolls independently, and the fixed areas remain visible.

## Pass/Fail Criteria

**Pass:**
- The header and bottom row are always visible while the history scrolls

**Fail:**
- The whole sidebar scrolls, or the bottom row is hidden or overlapped
