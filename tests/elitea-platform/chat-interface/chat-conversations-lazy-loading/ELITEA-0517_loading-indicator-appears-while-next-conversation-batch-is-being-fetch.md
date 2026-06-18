---
id: ELITEA-0517
title: "Loading Indicator Appears While Next Conversation Batch Is Being Fetched"
priority: medium
type: functional
module: chat-conversations-lazy-loading
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4834]
---
# ELITEA-0517: Loading Indicator Appears While Next Conversation Batch Is Being Fetched

**Module:** Chat Conversations Lazy Loading · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a visible loading indicator appears while a new batch is being fetched, and disappears once loading completes.

**Coverage:**
- Spinner/skeleton visible at the bottom of the list during fetch
- Indicator disappears after conversations are appended
- No UI freeze during fetch

## Preconditions

- Logged in to {{base_url}} in a project requiring scroll to load more
- DevTools → Network → Throttling set to Slow 3G to slow down and reveal indicator reliably

## Test Data

- Throttling: Slow 3G (DevTools → Network → No throttling → select "Slow 3G")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Slow 3G throttling in DevTools. Navigate to Chat. | Initial batch loads (slowly). |
| 2 | Scroll to the bottom of any conversation section. | A loading indicator (spinner, skeleton, or 'Loading…') appears at the bottom of the list. |
| 3 | Wait for the batch to complete. | Indicator disappears; new conversations appear below. |

## Expected Final State

Indicator disappears; new conversations appear below.

## Pass/Fail Criteria

**Pass:**
- Visible loading indicator shown during fetch
- Indicator disappears after load
- Sidebar remains scrollable during fetch

**Fail:**
- No indicator of any kind (blank space or immediate freeze)
- UI freezes during batch fetch
