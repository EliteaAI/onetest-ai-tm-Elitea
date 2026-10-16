---
id: ELITEA-4070
title: "Import JSON uploads valid theme file and applies settings correctly"
priority: high
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, import, json]
requirements: []
---

# ELITEA-4070: Import JSON uploads valid theme file and applies settings correctly

**Module:** admin-portal/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that the Import JSON functionality correctly parses a valid theme JSON file and applies all settings to the Custom Theme configuration UI.

---

## Preconditions

- User has Admin role with access to Admin Portal
- Have a valid theme JSON file ready (previously exported or manually created)
- JSON file contains valid color values and structure
- Current Custom Theme has different values than the import file

---

## Test Data

| Field | Value |
|-------|-------|
| Import file Primary Main | #E74C3C (red) |
| Import file Secondary Main | #2ECC71 (green) |
| Current Primary Main (before import) | Different from import values |

Sample valid JSON structure:
```json
{
  "baseMode": "dark",
  "primaryMain": "#E74C3C",
  "secondaryMain": "#2ECC71",
  "backgroundColors": {...},
  "borderColors": {...}
}
```

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log into Admin Portal as admin user | Admin Portal loads successfully |
| 2 | Navigate to Features → Custom Theme | Custom Theme configuration page loads |
| 3 | Note current Primary Main color value | Current value is different from import file |
| 4 | Locate "Import JSON" button in the top toolbar | Import JSON button is visible |
| 5 | Click "Import JSON" button | File picker dialog opens |
| 6 | Select the valid theme JSON file | File is selected |
| 7 | Confirm file selection | Import process initiates |
| 8 | Observe UI update | Theme configuration UI updates with imported values |
| 9 | Expand Primary Colors section | Section shows color values |
| 10 | Verify Primary Main shows #E74C3C | Color picker/input displays imported value |
| 11 | Verify Secondary Main shows #2ECC71 | Color picker/input displays imported value |
| 12 | Verify other imported sections reflect JSON values | All imported categories show correct values |
| 13 | Click "Save Changes" to persist imported configuration | Save completes successfully |
| 14 | Refresh the page | Page reloads |
| 15 | Verify imported values persist after refresh | All imported values are retained |

---

## Expected Final State

All values from the imported JSON file are applied to the Custom Theme configuration and persist after saving, ready to be used by users selecting Project theme.

---

## Pass/Fail Criteria

**Pass:**
- Import JSON button opens file picker
- Valid JSON file is accepted and parsed
- All UI fields update to reflect imported values
- Color pickers show correct imported colors
- Imported configuration can be saved successfully
- Values persist after page refresh

**Fail:**
- File picker fails to open
- Valid JSON file is rejected
- UI does not update after import
- Imported values are incorrect or missing
- Save operation fails after import
- Values lost after page refresh
