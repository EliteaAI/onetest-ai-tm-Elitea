---
id: ELITEA-1120
title: "QTest Toolkit – \"Add file to test case\" Tool Present, Toggleable, and Executes Successfully"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, feat:toolkits]
requirements: [3180]
---
# ELITEA-1120: QTest Toolkit – "Add file to test case" Tool Present, Toggleable, and Executes Successfully

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the new "Add file to test case" tool is visible in the QTest toolkit panel, can be enabled/disabled, and successfully uploads a file to a QTest test case using an Artifact bucket path.

## Preconditions

- ELITEA platform accessible at {{base_url}}
- User is logged in with valid credentials
- QTest toolkit is configured with valid credentials
- An Artifact Toolkit bucket exists with at least one file (e.g., /my-bucket/test-file.png)
- A valid QTest test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA → Toolkits → QTest toolkit configuration page | QTest toolkit settings panel is displayed |
| 2 | Scroll through the available tools list and locate 'Add file to test case' | 'Add file to test case' tool is visible in the tools list |
| 3 | Toggle the 'Add file to test case' tool OFF, save, then toggle it ON and save again | Tool toggles without error; enabled state persists after save |
| 4 | Invoke the 'Add file to test case' tool with a valid test_case_id and filepath (e.g., /my-bucket/test-file.png) | Tool executes without error and returns a success response |
| 5 | Navigate to QTest and open the test case used in step 4 | The file (test-file.png) appears as an attachment on the QTest test case |

## Expected Final State

The file (test-file.png) appears as an attachment on the QTest test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
