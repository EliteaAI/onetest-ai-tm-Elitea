---
id: ELITEA-0519
title: "Toolkit Test Settings chat — scrollbar visible and functional when tool response overflows the panel"
priority: medium
type: functional
module: chat-scrollbar
status: ready
execution_type: manual
tags: [feat:toolkits, issue:3704, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3704]
---
# ELITEA-0519: Toolkit Test Settings chat — scrollbar visible and functional when tool response overflows the panel

**Module:** Chat Scrollbar · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a scrollbar is visible and functional in the Toolkit Test Settings chat result area when API tool responses overflow the visible area.

**Coverage:**
- Scrollbar appears in the Toolkit Test Settings chat panel when tool output overflows
- Dragging the scrollbar thumb scrolls the chat result content
- Mouse wheel scrolling works within the Test Settings chat area
- Full tool response content is reachable by scrolling

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A Toolkit configured with working credentials (e.g., Jira, GitHub, or Artifacts toolkit)
- The toolkit has a tool that returns verbose output (e.g., list issues, list files, list branches)
- Chrome or Edge, latest stable

## Test Data

- Toolkit: any toolkit returning verbose output (e.g., Artifacts `ListFiles` with many files, or Jira `ListIssues`)
- Example: Artifacts toolkit → Test Settings → ListFiles → Bucket with many files

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits. Open a configured toolkit (e.g., Jira or Artifacts). Click the gear icon or navigate to Test Settings on the right panel. | Test Settings panel opens with a tool selector and a chat/result area below. |
| 2 | Select a tool that returns a large list response (e.g., ListFiles on an Artifacts toolkit with many files, or list_issues on Jira). Click Run. | Tool executes and returns a verbose response in the chat area. |
| 3 | Observe the right edge of the Test Settings chat result area. | A scrollbar is visible on the right side of the chat result panel. |
| 4 | Click and drag the scrollbar thumb upward and downward. | Content in the chat result area scrolls correctly with the thumb. |
| 5 | Place the cursor over the chat result area and use the mouse wheel. | Content scrolls smoothly using the mouse wheel. |
| 6 | Scroll to the bottom of the result area. | The end of the tool response is fully visible; no content is hidden below the panel. |

## Expected Final State

The end of the tool response is fully visible; no content is hidden below the panel.

## Pass/Fail Criteria

**Pass:**
- Scrollbar visible in Test Settings chat area after a verbose tool response
- Dragging and wheel scrolling both work correctly
- All tool response content accessible by scrolling

**Fail:**
- No scrollbar after verbose tool output (original reported bug)
- Content overflows with no scroll mechanism — user cannot read the full response
- Scrollbar visible but non-functional
