---
id: ELITEA-1771
title: "SharePoint Personal URL — Read .docx File from Sharing Link"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, file-operations, docx, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1771: SharePoint Personal URL — Read .docx File from Sharing Link

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the SharePoint toolkit successfully retrieves and extracts text content from .docx Word documents stored in personal SharePoint using sharing links.

## Preconditions

- Personal SharePoint credential configured and connected
- .docx file (< 10MB) uploaded to personal SharePoint
- Sharing link generated for the .docx file
- Agent configured with SharePoint toolkit

## Test Data

- Test file: `test-document.docx` with formatted content (headings, paragraphs, lists)
- Sharing link format: `https://your-tenant-my.sharepoint.com/:w:/p/username/...`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat with SharePoint-enabled agent | Chat interface opens |
| 2 | Send message: "Read the Word document from: [personal-sharepoint-docx-sharing-link]" | Agent processes request |
| 3 | Agent invokes "Read file from sharing link" tool | Tool execution starts |
| 4 | Wait for document processing | Tool completes within 15 seconds |
| 5 | Observe extracted content in response | Document text content displayed; Headings and paragraph structure preserved |
| 6 | Verify formatting elements captured | Lists, bold/italic indicators visible in extracted text |

## Expected Final State

Document text content successfully extracted with formatting preserved

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Text content extracted from .docx file
- Document structure (headings, paragraphs) preserved
- No error messages

**Fail:**
- Tool returns error
- Empty response or partial content extraction
- Content corruption or encoding issues
