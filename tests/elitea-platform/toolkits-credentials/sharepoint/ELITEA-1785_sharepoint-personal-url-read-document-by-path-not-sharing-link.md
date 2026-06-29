---
id: ELITEA-1785
title: "SharePoint Personal URL — Read Document by Path (Not Sharing Link)"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, document-path, file-operations, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1785: SharePoint Personal URL — Read Document by Path (Not Sharing Link)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that SharePoint toolkit can read documents from personal SharePoint using document path (not only sharing links).

## Preconditions

- Personal SharePoint credential configured
- File uploaded to known path in personal SharePoint (e.g., `/Documents/test-file.pdf`)
- Agent configured with SharePoint toolkit

## Test Data

- Document path: `/Documents/test-file.pdf` or `/Shared Documents/report.docx`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat opens |
| 2 | Send message: "Read the document at /Documents/test-file.pdf" | Agent invokes "Read document" tool (by path parameter) |
| 3 | Wait for tool execution | Tool processes |
| 4 | Observe response | File located and retrieved; Content displayed in response; Works for both absolute and relative paths; No error: "Path not supported" |

## Expected Final State

Document content successfully retrieved using path

## Pass/Fail Criteria

**Pass:**
- Tool accepts document path parameter
- File located and retrieved by path
- Content displayed
- Both absolute and relative paths work

**Fail:**
- Tool rejects path parameter
- "Path not supported" error
- Only sharing links work, paths don't
