---
id: ELITEA-3800
title: "SharePoint Personal URL — Read .txt File from Sharing Link"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, file-operations, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-3800: SharePoint Personal URL — Read .txt File from Sharing Link

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the SharePoint toolkit successfully retrieves and extracts content from .txt files stored in personal SharePoint using sharing links.

## Preconditions

- Personal SharePoint credential configured and connected
- .txt file (< 5MB) uploaded to personal SharePoint account
- Sharing link generated for the .txt file
- Agent configured with SharePoint toolkit attached

## Test Data

- Test file: `sample-text.txt` containing: "This is a test file for personal SharePoint URL support."
- Sharing link format: `https://epam-my.sharepoint.com/:t:/p/username/...`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat or select agent with SharePoint toolkit | Chat interface opens |
| 2 | Send message: "Read the file from this link: [personal-sharepoint-txt-sharing-link]" | Agent processes the request |
| 3 | Agent invokes "Read file from sharing link" tool | Tool execution starts, loading indicator appears |
| 4 | Wait for file content extraction | Tool completes within 10 seconds |
| 5 | Observe response content | File text content displayed in agent response: "This is a test file for personal SharePoint URL support." |
| 6 | Verify no error messages displayed | Response shows success, no errors |

## Expected Final State

File content successfully extracted and displayed in agent response

## Pass/Fail Criteria

**Pass:**
- Tool executes without errors
- File content extracted matches original .txt file
- Response displays full text content
- Execution time < 10 seconds

**Fail:**
- Tool returns error (404, access denied, unsupported URL)
- File content incomplete or corrupted
- Empty response box
