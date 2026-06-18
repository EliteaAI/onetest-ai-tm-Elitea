---
id: ELITEA-0628
title: "Support Assistant entry in collapsed sidebar shows a visible icon, not an invisible click area"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [collapsed-sidebar, discoverability, icon]
requirements: [EliteaAI/elitea_issues#4780]
---
# ELITEA-0628: Support Assistant entry in collapsed sidebar shows a visible icon, not an invisible click area

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** When the sidebar is collapsed to icon-only mode, users rely entirely on icons to navigate. If the Support Assistant entry renders as an invisible block (no icon visible), users in collapsed sidebar mode will have no way to know the feature exists or how to open it.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant feature is enabled
Sidebar is currently in expanded mode showing the "Support Assistant" text label

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate the "Support Assistant" entry at the bottom of the expanded sidebar. Confirm it shows the text label and an icon. | Entry visible with icon and "Support Assistant" label. |
| 2 | Click the sidebar collapse control at the top of the sidebar to collapse it to icon-only mode. | Sidebar switches to icon-only mode. All standard nav items show only their icons. |
| 3 | Look at the bottom of the collapsed sidebar where the Support Assistant entry was. | A visible icon for the Support Assistant is present at the same position — it is not an empty or invisible area. |
| 4 | Hover the mouse over the Support Assistant icon in the collapsed sidebar. | A tooltip appears with the text "Support Assistant". |
| 5 | Click the Support Assistant icon while the sidebar is in collapsed mode. | The Support Assistant panel opens normally, exactly as it does in expanded mode. |

## Expected Final State

The Support Assistant panel opens normally, exactly as it does in expanded mode.

## Pass/Fail Criteria

Pass: A visible icon is shown for the Support Assistant entry in collapsed sidebar mode; Hovering the icon shows a "Support Assistant" tooltip; Clicking the icon opens the panel normally.
Fail: The Support Assistant entry has no visible icon in collapsed mode (appears as a blank space); No tooltip appears on hover; The click area is invisible and users cannot discover or open the feature in collapsed sidebar mode.
