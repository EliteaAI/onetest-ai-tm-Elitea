---
id: ELITEA-0935
title: "UI — Character Count, Mode Labels, and Upload Button Are Functional"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, story:3395, r-2.0.4, ui-ux]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0935: UI — Character Count, Mode Labels, and Upload Button Are Functional

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the character count updates in real-time, mode labels are always visible, mode switching is smooth, and the Upload button is discoverable.

**Coverage:**
- Real-time character count
- Editor/Preview mode label always shown
- Smooth mode switch
- Upload button visible and labeled

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Project Context editor. Type several characters one at a time. | Character count updates with every keystroke in real-time. |
| 2 | Check for a mode label on the page. | 'Editor' or 'Preview' label/indicator is visible. |
| 3 | Click the Preview mode button. Observe the transition. | Mode switches smoothly with no full page reload. Label now shows 'Preview'. |
| 4 | Click back to Editor mode. | Mode returns to Editor. Raw Markdown is editable again. |
| 5 | Look for the Upload button on the page. | Upload button is clearly visible, has a label, and is easy to find without searching. |
| 6 | Add enough content to require scrolling. Scroll the page. | Page scrolls correctly. No layout overflow or content clipping. |

## Expected Final State

Page scrolls correctly. No layout overflow or content clipping.

## Pass/Fail Criteria

**Pass:**
- Count updates on every keystroke
- Mode label visible at all times
- No page reload on mode switch
- Upload button clearly visible

**Fail:**
- Count is delayed or only updates on save
- Mode label absent
- Page reloads on mode switch
- Upload button hidden or missing
