---
id: ELITEA-1119
title: "Jira Toolkit – \"Add file to issue description\" Tool Present, Toggleable, and Executes Successfully"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits]
requirements: [3180]
---
# ELITEA-1119: Jira Toolkit – "Add file to issue description" Tool Present, Toggleable, and Executes Successfully

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the new "Add file to issue description" tool is visible in the Jira toolkit panel, can be enabled/disabled, and successfully uploads a file to a Jira issue description field using an Artifact bucket path.

## Preconditions

- ELITEA platform accessible at {{base_url}}
- User is logged in with valid credentials
- Jira toolkit is configured with valid credentials
- An Artifact Toolkit bucket exists with at least one file (e.g., /my-bucket/test-file.png)
- A valid Jira issue key is available (e.g., PROJ-123)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA → Toolkits → Jira toolkit configuration page | Jira toolkit settings panel is displayed |
| 2 | Scroll through the available tools list and locate 'Add file to issue description' | 'Add file to issue description' tool is visible in the tools list |
| 3 | Toggle the 'Add file to issue description' tool OFF, save, then toggle it ON and save again | Tool toggles without error; enabled state persists after save |
| 4 | Invoke the 'Add file to issue description' tool with a valid issue_key and filepath (e.g., /my-bucket/test-file.png) | Tool executes without error and returns a success response |
| 5 | Navigate to Jira and open the issue used in step 4 | The file reference appears in the Jira issue description field |

## Expected Final State

The file reference appears in the Jira issue description field

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
