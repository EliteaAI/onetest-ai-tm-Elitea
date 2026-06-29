---
id: ELITEA-1782
title: "SharePoint Personal URL — .docx Embedded Objects Extraction"
priority: high
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, docx, embedded-objects, bug-5333, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054, EliteaAI/elitea_issues#5333]
---
# ELITEA-1782: SharePoint Personal URL — .docx Embedded Objects Extraction

**Module:** Sharepoint · **Priority:** High · **Type:** Regression

**Objective:** Verify that SharePoint toolkit extracts embedded objects (charts, textboxes, flowcharts, images) from .docx files in personal SharePoint.

**Bug Coverage:** Regression test for bug #5333 — Embedded objects not extracted

## Preconditions

- Personal SharePoint credential configured
- .docx file with embedded objects uploaded: charts, textboxes, flowcharts, images
- Example: bubblesort_diagram.docx with flowchart
- Sharing link generated
- Agent configured with SharePoint toolkit

## Test Data

- Test file: `diagram-document.docx` containing embedded flowchart or diagram

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat opens |
| 2 | Send message: "Read this document and describe the diagram: [docx-with-embedded-objects-link]" | Agent invokes tool |
| 3 | Wait for processing | Tool completes |
| 4 | Observe extracted content | Document text content extracted; Embedded object alternative text/descriptions included; Chart titles and labels extracted; Textbox content included; Complete document structure preserved |
| 5 | Verify no silent skip of embedded content | Embedded elements acknowledged in extraction |

## Expected Final State

Document text and embedded object content successfully extracted

## Pass/Fail Criteria

**Pass:**
- Tool extracts text content from document
- Embedded object descriptions or alt text included
- Chart/textbox content captured
- No silent skip of embedded elements
- Complete document structure preserved

**Fail:**
- Embedded objects completely ignored in extraction
- Only plain text extracted, diagrams/charts missing
- Incomplete document content
