---
id: ELITEA-1167
title: "TC-011: Confluence Advanced Fields (Retry Settings + Custom Headers) Are Persisted After Save and Reopen"
priority: high
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1167: TC-011: Confluence Advanced Fields (Retry Settings + Custom Headers) Are Persisted After Save and Reopen

**Module:** Confluence Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that values entered in Confluence Advanced Settings fields (retry settings and Custom Headers) are persisted after saving the toolkit and reopening it.

Coverage:
- Number of Retries, Min/Max Retry Seconds can be set and are saved correctly
- Custom Headers key-value pairs entered are saved and shown on reopen
- Data survives a full save → close → reopen cycle

## Preconditions

- Logged in as User A
- Confluence toolkit creation form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Confluence toolkit creation form and fill all required fields | Form accepts input |
| 2 | Expand Advanced Settings | Max Pages, Number of Retries, Min Retry Seconds, Max Retry Seconds, Custom Headers visible |
| 3 | Set Number of Retries to 5, Min Retry Seconds to 2, Max Retry Seconds to 30 | Values accepted |
| 4 | Add a Custom Headers key-value pair: key 'X-Test-Key', value 'abc123' | Entry accepted |
| 5 | Save the toolkit | Toolkit saved successfully |
| 6 | Close the form and reopen the saved toolkit | Form opens with all fields loaded |
| 7 | Expand Advanced Settings and verify all entered values | Number of Retries = 5, Min Retry Seconds = 2, Max Retry Seconds = 30, Custom Headers entry present with correct key/value |

## Expected Final State

Number of Retries = 5, Min Retry Seconds = 2, Max Retry Seconds = 30, Custom Headers entry present with correct key/value

## Pass/Fail Criteria

PASS:
- After save and reopen, retry fields (Number of Retries, Min/Max Retry Seconds) reflect the values set before save
- After save and reopen, Custom Headers key-value pairs are present and correct

FAIL:
- Retry fields revert to default after save/reopen
- Custom Headers are blank or missing on reopen
- Save operation returns an error
