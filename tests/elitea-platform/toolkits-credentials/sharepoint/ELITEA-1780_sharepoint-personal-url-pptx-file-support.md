---
id: ELITEA-1780
title: "SharePoint Personal URL — PowerPoint .pptx File Support"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, pptx, file-support, bug-5299, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5299]
---
# ELITEA-1780: SharePoint Personal URL — PowerPoint .pptx File Support

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that SharePoint toolkit successfully reads .pptx PowerPoint files from personal SharePoint sharing links without errors.

**Bug Coverage:** Regression test for bug #5299 — .pptx file reading failure

## Preconditions

- Personal SharePoint credential configured
- .pptx file uploaded to personal SharePoint (5-10 slides with text)
- Sharing link generated
- Agent configured with SharePoint toolkit

## Test Data

- Test file: `presentation.pptx` with slide titles and bullet points

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat opens |
| 2 | Send message: "Read the PowerPoint from: [pptx-sharing-link]" | Agent invokes "Read file from sharing link" |
| 3 | Wait for processing | Tool completes within 20 seconds |
| 4 | Observe extracted content | Slide text content extracted; Slide titles included; Bullet points or body text visible; No error: "Failed to read .pptx file" |
| 5 | Verify readability of content | Content is readable and structured |

## Expected Final State

PowerPoint slide content successfully extracted and displayed

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully (no error)
- Slide text content extracted
- Titles and body text included
- Response displays readable slide content

**Fail:**
- Error: "Failed to read .pptx file" or "Unsupported format"
- Empty response
- Content extraction fails
