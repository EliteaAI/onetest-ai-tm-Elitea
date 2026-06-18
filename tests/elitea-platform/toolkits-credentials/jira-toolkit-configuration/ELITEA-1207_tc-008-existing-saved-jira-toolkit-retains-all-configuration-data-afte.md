---
id: ELITEA-1207
title: "TC-008: Existing Saved Jira Toolkit Retains All Configuration Data After UI Reorganization"
priority: critical
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1207: TC-008: Existing Saved Jira Toolkit Retains All Configuration Data After UI Reorganization

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an existing Jira toolkit that was saved before the UI reorganization still displays all its configuration data correctly after the change is deployed. All 8 visible fields must populate with the stored values, and Advanced Settings must expose the saved Verify SSL + Custom Headers values when expanded.

Coverage:
- Pre-existing saved Jira toolkit opens without error
- All 8 visible fields populate with correct saved values
- Advanced Settings section is present and expandable
- Expanded Advanced Settings shows correct saved Verify SSL state + Custom Headers values
- No field data is lost or blank unexpectedly

## Preconditions

- A Jira toolkit that was created and saved before the UI reorganization exists in the project
- Logged in as the toolkit owner

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the existing pre-change Jira toolkit and open it for edit | Toolkit form opens without errors |
| 2 | Verify the 8 visible field values: Toolkit Name, Jira URL, Username/Email, Token, Connection Type, Project, Issue Type, Status | All 8 fields are populated with the values that were saved before the change |
| 3 | Confirm the 'Cloud checkbox' is gone — it should no longer appear on the form | No Cloud checkbox is visible |
| 4 | Click 'Advanced Settings' to expand it | Section expands with Verify SSL, Additional Fields, Custom Headers visible |
| 5 | Check Verify SSL toggle state matches what was saved originally | Verify SSL toggle reflects the original saved value |
| 6 | Check Custom Headers values | Custom Headers shows previously saved key-value pairs without loss |

## Expected Final State

Custom Headers shows previously saved key-value pairs without loss

## Pass/Fail Criteria

PASS:
- Existing toolkit opens without error
- All 8 visible fields show their previously saved values
- Advanced Settings expands to reveal Verify SSL + Additional Fields + Custom Headers with correct values

FAIL:
- Toolkit fails to open or throws an error
- Any previously saved value is blank
- Advanced Settings is missing or does not expand
- Verify SSL or Custom Headers data is lost
