---
id: ELITEA-2223
title: "Help Center — Video Library \"More...\" redirects to full video portal"
priority: high
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2223: Help Center — Video Library \"More...\" redirects to full video portal

**Module:** help-center · **Priority:** high · **Type:** functional

**Objective:** Verify that Help Center — Video Library "More..." redirects to full video portal. Success is confirmed when verify videos are listed with thumbnails, titles, authors, and durations.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Help Center | Target page/section loads successfully. |
| 2 | Locate the VIDEO LIBRARY card (purple icon, subtitle: "Product walkthroughs and recorded sessions") | Action completes without error and produces the expected UI state. |
| 3 | Verify links displayed: Self-Service Agent Publishing, Clearer Shared Credential Setup, Indexing: Completion Summary Report, Notification Center: Inbox-Style Management, More... | Condition holds as described. |
| 4 | Click the "More..." link | Control responds; expected next state is shown. |
| 5 | Verify the user is redirected to the external Video Digital Platform portal | Condition holds as described. |
| 6 | Verify the portal displays the "Elitea - AI Collaborative Platform" channel page | Condition holds as described. |
| 7 | Verify the channel page shows available videos and playlists (e.g., Videos tab and Playlists tab) | Condition holds as described. |
| 8 | Verify videos are listed with thumbnails, titles, authors, and durations | Condition holds as described. |

---

## Expected Final State

Verify videos are listed with thumbnails, titles, authors, and durations.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Video Library "More..." redirects to full video portal.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
