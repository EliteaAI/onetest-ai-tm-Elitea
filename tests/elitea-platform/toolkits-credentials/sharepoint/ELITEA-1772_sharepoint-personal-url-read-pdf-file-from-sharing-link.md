---
id: ELITEA-1772
title: "SharePoint Personal URL — Read .pdf File from Sharing Link"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, file-operations, pdf, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1772: SharePoint Personal URL — Read .pdf File from Sharing Link

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the SharePoint toolkit successfully retrieves and extracts text content from .pdf files stored in personal SharePoint using sharing links.

## Preconditions

- Personal SharePoint credential configured and connected
- .pdf file (< 10MB, multiple pages) uploaded to personal SharePoint
- Sharing link generated for the .pdf file
- Agent configured with SharePoint toolkit

## Test Data

- Test file: `test-report.pdf` (5-10 pages with text content)
- Sharing link format: `https://epam-my.sharepoint.com/:b:/p/username/...`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat with SharePoint-enabled agent | Chat interface opens |
| 2 | Send message: "Extract text from this PDF: [personal-sharepoint-pdf-sharing-link]" | Agent processes request |
| 3 | Agent invokes "Read file from sharing link" tool | Tool execution starts, may show "Processing PDF..." |
| 4 | Wait for OCR/text extraction to complete | Tool completes within 30 seconds for multi-page PDF |
| 5 | Observe extracted content | PDF text content displayed in response box |
| 6 | Verify multi-page content included | Content from multiple pages extracted (page breaks may be indicated) |

## Expected Final State

PDF text content successfully extracted from all pages

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Text content extracted from PDF
- Multi-page content included
- Response box shows extracted text (not empty)

**Fail:**
- Tool returns error
- Empty response box (bug #5341 regression)
- Only first page extracted
- Content unreadable or corrupted
