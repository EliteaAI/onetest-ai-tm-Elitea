---
id: ELITEA-2941
title: "Toolkit Authorization Required popup renders correctly across light/dark mode and narrow screen widths"
priority: medium
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An OAuth-requiring toolkit (no valid token) can trigger the "Toolkit Authorization Required" popup
- Ability to toggle the application's light/dark theme and resize the browser viewport

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Theme variants | Light mode, Dark mode |
| Viewport variants | Standard desktop width, narrow/mobile width |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch the application to light mode and trigger the popup | Popup renders with correct contrast, readable text, and no clipped/overlapping elements |
| 2 | Switch the application to dark mode and trigger the popup | Popup renders with correct contrast, readable text, and no clipped/overlapping elements |
| 3 | Resize the browser to a narrow/mobile width and trigger the popup | Popup remains fully visible, readable, and usable (buttons reachable, text not truncated/overflowing) |
| 4 | Expand "Authorization details" at narrow width | Expanded content remains readable and does not break the layout |

## Expected Final State

The popup renders correctly and remains fully usable across both light/dark themes and narrow screen widths, with no visual defects.

## Pass/Fail Criteria

**Pass:**
- Popup is fully readable and usable in both light and dark mode
- Popup remains fully usable at narrow/mobile widths, including expanded Authorization details

**Fail:**
- Any theme shows poor contrast, unreadable text, or visual artifacts
- Narrow width causes clipped/overlapping/truncated content or unreachable buttons
