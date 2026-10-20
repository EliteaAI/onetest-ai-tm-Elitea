---
id: ELITEA-4123
title: "Verify catalog card layout and show-more control render correctly across viewports and browsers"
priority: high
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A published agent exists with a welcome message long enough to require "Show more"

## Test Data

| Viewport | Resolution |
|----------|------------|
| Desktop | 1920x1080 |
| Tablet | 768x1024 |
| Mobile | 375x812 |

| Browser |
|---------|
| Chrome (primary) |
| Firefox (secondary) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Agents Studio in Chrome at Desktop viewport and locate the test agent's card | Card is visible |
| 2 | Verify the "Show more" control is visible, unclipped, and does not overlap other card elements | Control renders correctly |
| 3 | Click "Show more" and verify the expanded text renders fully without layout breakage or horizontal scrolling | Expanded text is fully readable |
| 4 | Repeat steps 2–3 at Tablet viewport | Control and expanded text render correctly |
| 5 | Repeat steps 2–3 at Mobile viewport | Control and expanded text render correctly |
| 6 | Open Agents Studio in Firefox at Desktop viewport and repeat steps 2–3 | Control and expanded text render correctly |

## Expected Final State

The "Show more" control and its expanded content render correctly and legibly at all tested viewport/browser combinations.

## Pass/Fail Criteria

**Pass:**
- Control is visible and usable, and expanded text renders without clipping, overlap, or horizontal scroll at every tested viewport/browser combination

**Fail:**
- Control is hidden, clipped, or non-functional at any tested combination
- Expanded text causes layout breakage or requires horizontal scrolling
