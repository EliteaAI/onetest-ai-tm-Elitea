---
id: ELITEA-4911
title: "Verify sidebar layout holds at large and small window sizes"
priority: medium
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4911: Verify sidebar layout holds at large and small window sizes


## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has enough chats to overflow the sidebar

## Test Data

| # | Viewport | Note |
|---|----------|------|
| 1 | 1920 × 1080 | Large desktop |
| 2 | 1366 × 768 | Reference size |
| 3 | 1280 × 720 | Small window (triggers `useIsSmallWindow` on dev) |
| 4 | 1024 × 768 | Narrow window |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Resize the browser to the viewport from the Test Data row | The page re-renders |
| 2 | Check the expanded sidebar | Width is 288 px, all areas are visible, nothing overlaps or is cut off, and there's no horizontal page scroll |
| 3 | Check the Chats header | The "Chats" label and the Search / Create folder / Import icon buttons are shown the same way at every size, independent of `useIsSmallWindow` |
| 4 | Check the bottom row and chat history scroll | The bottom row stays fixed and visible, and the history scrolls independently |
| 5 | Collapse and expand the sidebar | Both states render correctly at this size |
| 6 | Repeat for every Test Data row | All sizes pass |

## Expected Final State

The sidebar is usable and consistent at every tested window size.

## Pass/Fail Criteria

**Pass:**
- No layout break, overlap or hidden control at any tested size
- The Chats header looks the same at all sizes

**Fail:**
- The Chats header changes form in a small window, or controls overflow or are hidden
