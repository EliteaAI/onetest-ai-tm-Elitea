---
id: ELITEA-1168
title: "TC-009: Existing Saved Confluence Toolkit Retains All Configuration Data After UI Reorganization"
priority: critical
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1168: TC-009: Existing Saved Confluence Toolkit Retains All Configuration Data After UI Reorganization

**Module:** Confluence Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an existing Confluence toolkit saved before the UI reorganization still displays all its configuration data correctly after the change is deployed. All 9 visible fields must be populated with original values, and Advanced Settings must expose the correct saved values.

Coverage:
- Pre-existing Confluence toolkit opens without error
- All 9 visible fields populated with original saved values
- Advanced Settings expands and shows correct saved values (Max Pages, Retry fields, Custom Headers)
- No data lost in migration

## Preconditions

- A Confluence toolkit saved before the UI reorganization exists in the project
- Logged in as the toolkit owner

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the existing pre-change Confluence toolkit for editing | Form opens without errors |
| 2 | Verify the 9 visible fields are populated with original values (Toolkit Name, Base URL, Username/Email, API Token, Space Keys, Connection Type, Cloud, Pages Limit, Labels) | All 9 fields show their previously saved values |
| 3 | Click 'Advanced Settings' to expand it | Section expands |
| 4 | Verify Max Pages value matches original | Correct saved value displayed |
| 5 | Verify Number of Retries, Min Retry Seconds, Max Retry Seconds values | All retry fields show originally saved values |
| 6 | Verify Custom Headers key-value pairs | Custom Headers shows originally saved entries without loss |

## Expected Final State

Custom Headers shows originally saved entries without loss

## Pass/Fail Criteria

PASS:
- Toolkit opens without errors
- All 9 visible fields show the originally saved values
- Advanced Settings expands and shows correct saved values

FAIL:
- Toolkit fails to open or shows an error
- Any previously saved field value is blank or reset
- Advanced Settings missing or saved retry/Custom Headers values are lost
