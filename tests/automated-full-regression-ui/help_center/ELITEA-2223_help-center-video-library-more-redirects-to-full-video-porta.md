---
id: ELITEA-2223
title: "Help Center — More... Links Expansion"
priority: high
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2223: Help Center — More... Links Expansion

**Module:** help-center · **Priority:** high · **Type:** functional

**Objective:** Verify that "More..." links on Video Library and Tutorials cards correctly redirect to their full content listings (video portal and complete tutorials list respectively), with expanded content displayed.

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
| **VIDEO LIBRARY "More..."** | | |
| 1 | Navigate to Help Center | Help Center page loads successfully |
| 2 | Locate the VIDEO LIBRARY card (purple icon, subtitle: "Product walkthroughs and recorded sessions") | Card is visible with correct icon and subtitle |
| 3 | Verify links displayed: Self-Service Agent Publishing, Clearer Shared Credential Setup, Indexing: Completion Summary Report, Notification Center: Inbox-Style Management, More... | Preview links and "More..." are visible |
| 4 | Click the "More..." link | Link is clickable |
| 5 | Verify the user is redirected to the external Video Digital Platform portal | Redirect occurs to video portal |
| 6 | Verify the portal displays the "Elitea - AI Collaborative Platform" channel page | Channel page is displayed |
| 7 | Verify the channel page shows available videos and playlists (e.g., Videos tab and Playlists tab) | Videos and playlists tabs are visible |
| 8 | Verify videos are listed with thumbnails, titles, authors, and durations | Video metadata is displayed correctly |
| **TUTORIALS "More..."** | | |
| 9 | Return to Help Center page | Help Center page is displayed |
| 10 | Locate the TUTORIALS card (green icon, subtitle: "Step-by-step guides and use cases") | Card is visible |
| 11 | Click the "More..." link at the bottom of the TUTORIALS card | Link is clickable |
| 12 | Verify the user is redirected to a page listing all available tutorials | Redirect occurs to full tutorials list |
| 13 | Verify the page loads without errors and displays more tutorials than shown in the card preview | Full tutorials list is displayed with expanded content |

---

## Expected Final State

Both "More..." links successfully expand to their full content: Video Library redirects to the video portal with channel page and video listings, and Tutorials redirects to the complete tutorials list with more items than the card preview.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Video Library "More..." redirects to video portal and displays channel page with videos/playlists metadata.
- Tutorials "More..." redirects to full list and displays more tutorials than the card preview.

**Fail:**
- Any step produces an error or unexpected result.
- Either "More..." link fails to redirect or expanded content is not displayed correctly.

---

## Notes

**Source functional tests:** ELITEA-2223 (Video Library "More..."), ELITEA-2224 (Tutorials "More...")

**Regression rationale:** Consolidates the "More..." expansion behavior into one test. Both links follow the same pattern: click "More..." → verify redirect to full listing → verify expanded content is displayed. Testing both expansion links validates the consistent "show more" UX pattern across different resource types.

**Selected checkpoints:** "More..." link visibility on both cards; redirect to external full listing; expanded content displays more items/details than card preview; Video Library specifically shows channel page with videos/playlists metadata.
