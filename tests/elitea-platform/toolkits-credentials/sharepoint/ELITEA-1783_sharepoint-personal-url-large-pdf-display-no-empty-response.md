---
id: ELITEA-1783
title: "SharePoint Personal URL — Large PDF Display (No Empty Response Box)"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, large-pdf, display-issue, bug-5341, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5341]
---
# ELITEA-1783: SharePoint Personal URL — Large PDF Display (No Empty Response Box)

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that reading large PDF files (15-19MB) from personal SharePoint displays extracted content in response box, not an empty box.

**Bug Coverage:** Regression test for bug #5341 — Empty response box for large PDFs

## Preconditions

- Personal SharePoint credential configured
- Large PDF file (15-19MB, close to size limit) uploaded to personal SharePoint
- Sharing link generated
- Agent configured with SharePoint toolkit

## Test Data

- Test file: `large-document.pdf` (17-19MB, multi-page)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat opens |
| 2 | Send message: "Read this PDF: [large-pdf-sharing-link]" | Agent invokes tool |
| 3 | Wait for processing (up to 60 seconds for large file) | Tool processes large PDF |
| 4 | Observe response box content | Response box displays extracted text (not empty); If truncated, shows first N characters with notice: "Content truncated..."; No silent failure with empty response |
| 5 | Verify content is readable | Text content visible and readable in response |

## Expected Final State

Large PDF content extracted and displayed (or clear truncation notice)

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Content extracted from large PDF
- Response box displays text (not empty)
- If truncated, clear truncation notice provided
- No silent failure

**Fail:**
- Empty response box despite successful extraction
- No content displayed
- Silent failure without error or truncation notice
