---
id: ELITEA-0520
title: "Chat Scrollbar visual consistency and layout — no content clipping, uniform styling across all three surfaces"
priority: medium
type: functional
module: chat-scrollbar
status: ready
execution_type: manual
tags: [feat:toolkits, issue:3704, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3704]
---
# ELITEA-0520: Chat Scrollbar visual consistency and layout — no content clipping, uniform styling across all three surfaces

**Module:** Chat Scrollbar · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the scrollbar is visually consistent with the ELITEA UI design and does not overlap or obscure message text, code blocks, or action buttons in any of the three chat surfaces.

**Coverage:**
- Scrollbar thumb, track, and hover state styling is uniform across Main Chat, Pipeline Chat, and Toolkit Test Settings chat
- No message content, code block line, or action icon is clipped or hidden under the scrollbar track
- No default OS-native scrollbar appearance that conflicts with the ELITEA theme

## Preconditions

- Logged in to {{base_url}}
- Long response loaded in each surface so the scrollbar is actively visible
- Chrome or Edge, latest stable
- Viewport at 1440px (default) and optionally 1280px

## Test Data

- Viewport widths: 1440px (default), 1280px
- Responses containing: long text paragraphs, a code block (markdown ``` block), and action buttons visible
- Compare: Main Chat vs Pipeline Chat vs Toolkit Test Settings chat scrollbar styling

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Load a long response in Main Chat so the scrollbar is active. Examine the scrollbar thumb and track: note color, width, and border-radius. | Scrollbar has a custom styled appearance matching the ELITEA dark theme (not a default gray OS scrollbar). |
| 2 | Hover over the scrollbar thumb in Main Chat. | A hover state is applied to the thumb (e.g., lighter color or increased opacity). |
| 3 | Inspect the right edge of the message bubbles — check whether any text characters, code block lines, or action icons (copy, thumbs up/down) are hidden or clipped under the scrollbar track. | All message content and action icons are fully visible; nothing is clipped by the scrollbar. |
| 4 | Navigate to Pipeline Chat panel with a loaded long conversation. Repeat the visual inspection from steps 1–3. | Scrollbar styling matches Main Chat. No content clipping observed. |
| 5 | Navigate to Toolkit Test Settings chat with verbose tool output. Repeat the visual inspection from steps 1–3. | Scrollbar styling consistent with the other two surfaces. No content clipping. |
| 6 | Resize the browser window to approximately 1280px width. Reload or regenerate a long response in each surface. Re-verify no content is clipped. | Layout holds at 1280px — scrollbar does not push content off-screen or overlap actionable elements. |

## Expected Final State

Layout holds at 1280px — scrollbar does not push content off-screen or overlap actionable elements.

## Pass/Fail Criteria

**Pass:**
- Scrollbar styling is visually uniform across all three surfaces
- No message text, code block content, or action button clipped under the scrollbar
- Scrollbar matches ELITEA design (not a default OS-style scrollbar)

**Fail:**
- Message text or action icons on the right side are partially hidden under the scrollbar track on any surface
- Significant styling inconsistency between surfaces (e.g., different track width, color, or border-radius)
- Default OS scrollbar displayed on one or more surfaces
