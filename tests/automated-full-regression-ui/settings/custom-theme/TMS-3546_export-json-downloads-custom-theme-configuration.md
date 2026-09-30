---
id: TMS-3546
title: "Export JSON downloads current custom theme configuration to file"
priority: high
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, export, json]
requirements: []
---

# TMS-3546: Export JSON downloads current custom theme configuration to file

**Module:** admin-portal/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that the Export JSON functionality in Custom Theme settings correctly exports all configured theme values to a downloadable JSON file that can be used for backup or sharing across environments.

---

## Preconditions

- User has Admin role with access to Admin Portal
- Custom theme has been configured with non-default values:
  - Custom Primary Main color set
  - Custom Secondary Main color set
  - Custom logo uploaded (optional but recommended)
- Browser allows file downloads

---

## Test Data

| Field | Value |
|-------|-------|
| Pre-configured Primary Main | #3FD99B |
| Pre-configured Secondary Main | #AEB984 |
| Expected file format | JSON |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log into Admin Portal as admin user | Admin Portal loads successfully |
| 2 | Navigate to Features → Custom Theme | Custom Theme configuration page loads |
| 3 | Verify custom values are currently configured | Primary Colors section shows non-default values |
| 4 | Locate "Export JSON" button in the top toolbar | Export JSON button is visible next to Import JSON |
| 5 | Click "Export JSON" button | File download initiates |
| 6 | Observe browser download behavior | JSON file downloads to browser's download folder |
| 7 | Locate downloaded file in downloads folder | File exists with .json extension |
| 8 | Open downloaded JSON file in text editor | File opens and displays JSON content |
| 9 | Verify JSON structure is valid (parseable) | JSON parses without syntax errors |
| 10 | Verify JSON contains "primaryMain" field with value #3FD99B | Primary Main color is present with correct value |
| 11 | Verify JSON contains "secondaryMain" field with value #AEB984 | Secondary Main color is present with correct value |
| 12 | Verify JSON contains base mode setting | Base mode (dark/light) is included |
| 13 | Verify JSON contains other color categories if configured | Background colors, border colors, etc. are included |

---

## Expected Final State

A valid JSON file is downloaded containing all custom theme configuration values including colors, logo reference, and base mode settings in a structure that can be imported back.

---

## Pass/Fail Criteria

**Pass:**
- Export JSON button triggers file download
- Downloaded file has .json extension
- JSON structure is valid and parseable
- All configured custom values are present in export
- Color values match what was configured in UI

**Fail:**
- Export button does not trigger download
- Downloaded file is corrupted or empty
- JSON structure is invalid
- Configured values are missing from export
- Color values do not match UI configuration
