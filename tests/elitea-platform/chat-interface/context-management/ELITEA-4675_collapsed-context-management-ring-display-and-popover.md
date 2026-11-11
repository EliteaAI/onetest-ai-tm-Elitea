---
id: ELITEA-4675
title: "Collapsed Context Management Ring: Display and Popover Controls"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Merge Note

Merges former draft cases "Collapsed panel shows a single ring indicator" and "Clicking the ring opens a popover" — the popover is simply what the ring opens into, not a separate feature; one flow covers display, content, and interaction.

## Preconditions

- User is logged in to `{{base_url}}`
- An active chat conversation with at least one message exchange exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an active chat conversation with the Participants panel expanded. | Context management card is visible at the bottom of the Participants panel. |
| 2 | Collapse the Participants panel (via the collapse control, or by narrowing the browser window below the panel's responsive breakpoint). | Participants panel collapses to a narrow rail. |
| 3 | Inspect the top-right area of the chat, under the panel-expand control, and its accessible label. | A circular progress ring is visible there, reflecting the current context usage percentage, with an accessible label such as "Context management N%". |
| 4 | Inspect the bottom of the collapsed rail for any legacy mini progress bar. | No bottom mini-bar or secondary "%" indicator exists anywhere else in the collapsed rail. |
| 5 | Click the circular ring. | A popover opens, anchored to the ring, showing: Context window Balanced/Full toggle, token usage line with percentage, Messages/Summaries counts, and the Usage totals section (Input tokens used, Output tokens used, Approx. cost). |
| 6 | Click the pencil/edit action inside the popover, then close the modal and use the quick Balanced/Full segmented toggle directly inside the popover. | The edit action opens the Context Management modal exactly as it would from the expanded card; the quick toggle switches window mode from within the popover with an optimistic UI update. |
| 7 | Press Escape while the popover is open; re-open it and click outside it. | Both Esc and click-outside close the popover. |
| 8 | Using only the keyboard, Tab to focus the ring, press Enter/Space to open the popover, then Tab through its controls. | The popover opens via keyboard activation alone, and focus moves through its interactive controls (toggle, edit icon) in a logical order. |
| 9 | Expand the Participants panel again (or widen the window). | The full Context management card reappears at the bottom of the expanded panel, as before. |
| 10 | Drive usage in this same conversation to ≥90% of usable input (e.g., per the ELITEA-4676 summarization-trigger flow), without yet reaching 100%. Collapse/expand the panel to directly compare the collapsed ring's color against the expanded card's color for the same conversation, without sending a message in between. | Both the ring and the expanded card show the same "warning" color state for the same underlying percentage — direct color parity, not just independently-correct colors. |
| 11 | Continue until usage reaches ≥100% of usable input. Again compare the ring's color against the expanded card's color for the same conversation. | Both the ring and the expanded card show the same "error" color state, matching each other. |

## Expected Final State

Exactly one context budget indicator (the bottom-right ring) is visible while collapsed; it opens a popover with complete, fully operable content by mouse and keyboard; the full card reappears correctly when the panel is expanded; and the ring's color matches the expanded card's color at both the warning (≥90%) and error (≥100%) thresholds for the same conversation (AC15 direct parity check).

## Pass/Fail Criteria

**Pass:**
- The ring appears in the top-right area when collapsed, with correct percentage and accessible label, and no duplicate/legacy bottom mini-bar
- Clicking or keyboard-activating the ring opens a popover whose content matches the expanded card exactly
- Edit and quick-switch controls work from within the popover; Esc and click-outside both close it
- Expanding the panel restores the full card correctly
- At both the ≥90% (warning) and ≥100% (error) thresholds, the ring's color directly matches the expanded card's color for the same conversation

**Fail:**
- The old bottom mini-bar is still present alongside or instead of the ring
- The ring is missing, mislabeled, or shows an incorrect percentage
- Popover fails to open via mouse or keyboard, or its content is incomplete/mismatched
- Esc or click-outside fails to close the popover
- The ring's color diverges from the expanded card's color at either the warning or error threshold
