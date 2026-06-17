---
id: ELITEA-1121
title: "Confluence Toolkit – \"Add file to page\" Tool Present, Toggleable, and Executes Successfully"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1121: Confluence Toolkit – "Add file to page" Tool Present, Toggleable, and Executes Successfully

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the new "Add file to page" tool is visible in the Confluence toolkit panel, can be enabled/disabled, and successfully uploads a file to a Confluence page using an Artifact bucket path.

## Preconditions

- ELITEA platform accessible at {{base_url}}
- User is logged in with valid credentials
- Confluence toolkit is configured with valid credentials
- An Artifact Toolkit bucket exists with at least one file (e.g., /my-bucket/test-file.png)
- A valid Confluence page ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA → Toolkits → Confluence toolkit configuration page | Confluence toolkit settings panel is displayed |
| 2 | Scroll through the available tools list and locate 'Add file to page' | 'Add file to page' tool is visible in the tools list |
| 3 | Toggle the 'Add file to page' tool OFF, save, then toggle it ON and save again | Tool toggles without error; enabled state persists after save |
| 4 | Invoke the 'Add file to page' tool with a valid page_id and filepath (e.g., /my-bucket/test-file.png) | Tool executes without error and returns a success response |
| 5 | Navigate to Confluence and open the page used in step 4 | The file (test-file.png) appears as an attachment on the Confluence page |

## Expected Final State

The file (test-file.png) appears as an attachment on the Confluence page

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
