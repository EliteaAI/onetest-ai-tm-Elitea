---
id: ELITEA-1089
title: "Banner visual styling matches the design specification"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1089: Banner visual styling matches the design specification

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the rendered warning banner matches the Figma design specification: red/warning border, ⓘ icon, bold prefix text, and hyperlink styling — across both light and dark themes.

**Coverage:**
- Banner border colour (palette.error.main)
- ⓘ icon presence
- Bold "Credential setup required:" text
- Underlined/accent-coloured "Create a credential" link
- No overlap with adjacent form elements
- Consistent appearance in light and dark themes

## Preconditions

- Logged in as **User B** with warning banner visible
- Browser: Chrome (latest)

## Test Data

- Theme variant: Light and Dark

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the team toolkit configuration as User B — banner is visible. | Warning banner is shown. |
| 2 | Verify the banner has a **red/warning-style border** using the error theme color. | Border is visually red/warning-colored, consistent with `palette.error.main`. |
| 3 | Verify the **ⓘ icon** is present on the left side of the banner. | Info/error icon (ⓘ) is visible. |
| 4 | Verify the prefix **"Credential setup required:"** is rendered in **bold**. | Text weight is visually heavier (bold) compared to the rest of the banner text. |
| 5 | Verify **"Create a credential"** is underlined and displayed in an accent/link color. | Hyperlink is underlined and uses the application's accent/link colour. |
| 6 | Verify the banner does not overlap or obscure adjacent form fields (URL, Authentication, etc.). | All form elements below the banner are fully visible and accessible. |
| 7 | Switch to **dark theme** and repeat steps 2–6. | Banner renders correctly in dark theme with appropriate colors. |
| 8 | Switch back to **light theme** and repeat steps 2–6. | Banner renders correctly in light theme. |

## Expected Final State

Banner renders correctly in light theme.

## Pass/Fail Criteria

**Pass:**
- All visual elements (border, icon, bold text, hyperlink) match design specification in both themes
- No overlap with adjacent form elements

**Fail:**
- Border is missing or uses wrong color
- ⓘ icon is absent
- "Credential setup required:" is not bold
- "Create a credential" is not a styled hyperlink
- Banner overlaps or hides form elements
