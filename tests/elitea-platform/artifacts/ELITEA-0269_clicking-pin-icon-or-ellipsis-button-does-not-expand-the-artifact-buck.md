---
id: ELITEA-0269
title: "Clicking pin icon or ellipsis button does not expand the artifact bucket"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: []
---
# ELITEA-0269: Clicking pin icon or ellipsis button does not expand the artifact bucket

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the pin icon or the ellipsis (⋮) context menu button on an artifact bucket does not expand the bucket to show its contents. Only clicking the bucket name/area itself should trigger expansion.

**Coverage:**
- Pin icon click toggles pin state only — does not expand the bucket
- Ellipsis (⋮) button click opens the context menu only — does not expand the bucket
- Bucket name/area click correctly expands the bucket (reference behavior)
- Behavior matches the chat folder pinning pattern (consistent UI interaction model)

## Preconditions

- User is logged in to ELITEA
- At least one artifact bucket exists in the sidebar (both pinned and unpinned state should be tested)
- The bucket is in a collapsed/non-expanded state at the start of each step group

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts section via the left sidebar | Artifacts page loads; bucket list is visible in the sidebar |
| 2 | Ensure an artifact bucket is in a collapsed (non-expanded) state — not currently showing its file contents | Target bucket is collapsed |
| 3 | Hover over the bucket row to reveal the pin icon (round/circle pin button) | Pin icon becomes visible on the bucket row without expanding the bucket |
| 4 | Click the pin icon on a currently unpinned bucket | Bucket pin state toggles (icon changes to filled/active); bucket does NOT expand to show its file contents; bucket moves to the top of the list if pinned |
| 5 | Verify the bucket remains collapsed after the pin action | Bucket contents (file list) are NOT visible; only the bucket row is shown |
| 6 | Hover over the same bucket row and click the pin icon again to unpin | Bucket unpins (icon reverts); bucket does NOT expand; bucket returns to regular list position |
| 7 | Hover over the bucket row and click the '...' (ellipsis) context menu button | The context menu opens showing options (Upload files, Pin to top, Edit, Delete); bucket does NOT expand to show its file contents |
| 8 | Dismiss the context menu (press Escape or click outside) | Context menu closes; bucket remains collapsed |
| 9 | Click directly on the bucket name/text area (not the pin icon or ellipsis) | Bucket expands and shows its file contents — this is the expected and only correct trigger for expansion |
| 10 | Navigate to a Chat section, hover over a chat folder, and use the pin icon to pin/unpin — observe for comparison | Chat folder does not expand when pin icon is clicked — confirming the expected UI pattern that bucket pinning should also follow |

## Expected Final State

Chat folder does not expand when pin icon is clicked — confirming the expected UI pattern that bucket pinning should also follow

## Pass/Fail Criteria

PASS:
- Pin icon click: bucket stays collapsed, pin state changes visually
- Ellipsis click: bucket stays collapsed, context menu appears
- Name/area click: bucket expands correctly
- No unintended expansion occurs during pin or menu interactions

FAIL:
- Bucket expands its file list when the pin icon is clicked
- Bucket expands its file list when the ellipsis button is clicked
- Pin state does not toggle when pin icon is clicked
