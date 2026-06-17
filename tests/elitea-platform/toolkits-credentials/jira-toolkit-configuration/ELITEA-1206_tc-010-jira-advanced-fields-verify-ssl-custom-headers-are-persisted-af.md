---
id: ELITEA-1206
title: "TC-010: Jira Advanced Fields (Verify SSL + Custom Headers) Are Persisted After Save and Reopen"
priority: high
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1206: TC-010: Jira Advanced Fields (Verify SSL + Custom Headers) Are Persisted After Save and Reopen

**Module:** Jira Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that values entered in Jira Advanced Settings fields (Verify SSL toggle state and Custom Headers key-value pairs) are persisted after saving the toolkit and reopening it.

Coverage:
- Verify SSL can be set and is saved correctly
- Custom Headers key-value pairs entered are saved and shown on reopen
- Data survives a full save → close → reopen cycle

## Preconditions

- Logged in as User A
- Jira toolkit creation form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Jira toolkit creation form and fill all required visible fields | Form accepts inputs |
| 2 | Expand Advanced Settings | Verify SSL, Additional Fields, Custom Headers visible |
| 3 | Toggle Verify SSL to a non-default state (e.g., enable it if disabled by default) | Toggle state changes |
| 4 | Add a Custom Headers key-value pair, e.g., key: 'X-Custom-Header', value: 'test-value' | Entry is accepted |
| 5 | Save the toolkit | Toolkit saved successfully |
| 6 | Close the form and reopen the saved toolkit | Toolkit form opens with all fields loaded |
| 7 | Expand Advanced Settings | Verify SSL toggle matches the value set before saving; Custom Headers shows the key-value pair that was entered |

## Expected Final State

Verify SSL toggle matches the value set before saving; Custom Headers shows the key-value pair that was entered

## Pass/Fail Criteria

PASS:
- After save and reopen, Verify SSL toggle reflects the value set before save
- After save and reopen, Custom Headers key-value pairs are present and correct

FAIL:
- Verify SSL reverts to default after save/reopen
- Custom Headers are blank or missing on reopen
- Save operation returns an error
