---
id: TMS-3544
title: "Admin can configure Primary Colors via color picker and hex input in Custom Theme"
priority: high
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, color-picker]
requirements: []
---

# TMS-3544: Admin can configure Primary Colors via color picker and hex input in Custom Theme

**Module:** admin-portal/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that administrators can configure Primary Main and Secondary Main colors in the Custom Theme settings using both the visual color picker and direct hex value input.

---

## Preconditions

- User has Admin role with access to Admin Portal
- User is logged into Admin Portal (dev.elitea.ai/admin)
- No unsaved changes exist in Custom Theme configuration

---

## Test Data

| Field | Value |
|-------|-------|
| Primary Main test color | #FF5733 (orange-red) |
| Secondary Main test color | #AEB984 (sage green) |
| Invalid hex value | #GGGGGG |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Portal → Features → Custom Theme | Custom Theme configuration page loads successfully |
| 2 | Verify Base Mode dropdown is present and functional | Dropdown shows Dark Mode/Light Mode options |
| 3 | Locate "Primary Colors" section (shows 2/2 colors indicator) | Primary Colors section is visible with expand/collapse control |
| 4 | Expand Primary Colors section if collapsed | Section expands showing Primary Main and Secondary Main fields |
| 5 | Click on Primary Main color picker swatch | Color picker modal/popover opens |
| 6 | Select color #FF5733 using the color picker | Color picker shows selected color; preview swatch updates |
| 7 | Verify hex input field updates to #FF5733 | Hex input field displays #FF5733 |
| 8 | Close color picker and verify swatch shows new color | Primary Main swatch displays #FF5733 |
| 9 | Click on Secondary Main hex input field | Input field becomes editable |
| 10 | Clear existing value and type #AEB984 | Hex value is entered in the field |
| 11 | Click outside the input or press Tab | Color swatch updates to reflect #AEB984 |
| 12 | Click "Save Changes" button | Save operation initiates with loading indicator |
| 13 | Verify success notification appears | Success toast/notification confirms save |
| 14 | Refresh the page | Page reloads |
| 15 | Verify Primary Main shows #FF5733 and Secondary Main shows #AEB984 | Both color values persist after refresh |

---

## Expected Final State

Both Primary Main (#FF5733) and Secondary Main (#AEB984) colors are saved and persist after page refresh, ready to be applied to users who select Project theme.

---

## Pass/Fail Criteria

**Pass:**
- Color picker opens and allows color selection
- Hex input accepts valid hex color codes
- Color preview swatches update in real-time
- Changes persist after save and page refresh
- Both selection methods (picker and hex input) work correctly

**Fail:**
- Color picker fails to open or select colors
- Hex input rejects valid color codes
- Color values do not persist after save
- Visual preview does not match entered values
