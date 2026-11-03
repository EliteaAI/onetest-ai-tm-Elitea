---
id: ELITEA-4327
title: "Download Button Visual Placement and Accessibility in Code Block Toolbar"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- A chat conversation exists with an AI response containing a code block and a separate tool-execution result rendered as a chip (touchpoint vs ELITEA-2210)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt | "Give me a short json config example" |
| Prompt (tool output chip scenario) | A prompt that triggers a toolkit/tool call so a tool-output chip renders near a code block (e.g. "List the files in my connected repository") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat`, open a conversation, and send the json prompt | AI responds with a code block showing Edit code, Copy code, and Download icons in its toolbar |
| 2 | Visually inspect the toolbar icon order, spacing, and sizing | Download icon is clearly distinguishable from Edit code/Copy code, with consistent spacing and no visual overlap between icons |
| 3 | Hover over the Download icon | A distinct tooltip/label (e.g. "Download") appears, clearly identifying the action and distinct from the Copy code tooltip |
| 4 | Use Tab/keyboard navigation to move focus through the code block toolbar | Download icon receives visible keyboard focus in a logical tab order alongside Edit code/Copy code |
| 5 | With the Download icon focused, press Enter or Space | The download action activates via keyboard, identical to a mouse click |
| 6 | Send the tool-output-chip prompt and observe the layout where a code block, its toolbar, and a tool-output chip (re-validation touchpoint vs ELITEA-2210) are near each other | The Download icon and its toolbar do not overlap, obscure, or get obscured by the tool-output chip rendering |

## Expected Final State

The Download icon is visually distinct, properly labeled, keyboard-accessible, and does not overlap with other toolbar icons or nearby tool-output chips.

## Pass/Fail Criteria

**Pass:**
- Download icon has a distinct tooltip/label from other toolbar actions
- Download icon is reachable and activatable via keyboard (Tab + Enter/Space)
- No visual overlap between the Download icon, other toolbar icons, or tool-output chips

**Fail:**
- Download icon lacks a tooltip/label or is visually indistinguishable from other icons
- Download icon cannot be focused or activated via keyboard
- Download icon or toolbar visually overlaps with other icons or tool-output chips (ELITEA-2210 regression)
