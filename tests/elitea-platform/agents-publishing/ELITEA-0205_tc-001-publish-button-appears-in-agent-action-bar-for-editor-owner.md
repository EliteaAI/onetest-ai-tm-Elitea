---
id: ELITEA-0205
title: "TC-001: Publish Button Appears in Agent Action Bar for Editor/Owner"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0205: TC-001: Publish Button Appears in Agent Action Bar for Editor/Owner

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a user with editor/owner permissions sees an enabled "Publish" button in the agent action bar — every agent always has at least a "base" saved version, so the button must always be accessible to editors/owners.

Coverage:
- Publish button visible and enabled on any agent ("base" version always exists)
- Button appears in the top action bar alongside Save / Save As Version / Discard controls
- Clicking the Publish button opens the Publish version modal (not a direct action)

## Preconditions

- Logged in as User A (editor/owner) on {{base_url}}
- Agent A exists (automatically has a "base" saved version)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents → open Agent A detail page | Agent A detail page loads; action bar is visible at the top |
| 2 | Inspect the top action bar for a 'Publish' button | A 'Publish' button is present in the action bar |
| 3 | Verify the 'Publish' button is enabled (not greyed out) and clickable | Button is interactive; cursor changes to pointer on hover |
| 4 | Click the 'Publish' button | The 'Publish version' modal opens — no direct publish action is taken |

## Expected Final State

The 'Publish version' modal opens — no direct publish action is taken

## Pass/Fail Criteria

PASS:
- "Publish" button is visible and enabled on Agent A
- Clicking the button opens the Publish version modal (does not publish immediately)
- No JavaScript error in the browser console when clicking the Publish button

FAIL:
- "Publish" button is missing on any agent owned by the logged-in editor
- Clicking Publish triggers an immediate publish action without opening a modal
- Page crashes or throws an unhandled error when clicking Publish
