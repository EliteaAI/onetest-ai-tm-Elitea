---
id: ELITEA-4810
title: "Share Chat window server errors and recovery"
priority: medium
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4810: Share Chat window server errors and recovery

**Module:** conversations · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Share Chat window handles failed requests without losing data.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1. DevTools is available to block or throttle requests.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Block the links list request and open Share > Externally | "Failed to load the links of this chat." with "Try again"; after unblocking, Try again loads the list |
| 2 | On Team add a person, block the save request, click Save | An error toast; the window stays open with the unsaved list; no "Access updated" |
| 3 | Unblock and click Save again | Saved; toast "Access updated" |
| 4 | Make Generate Link fail, then Revoke fail | Error toasts; no card is added or removed; counts unchanged |
| 5 | Check the Console | No unhandled errors |

---

## Expected Final State

Failures are reported clearly and can be retried without data loss.
