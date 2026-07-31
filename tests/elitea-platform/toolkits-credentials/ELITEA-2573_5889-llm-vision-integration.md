---
id: ELITEA-2573
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: LLM Vision Integration & Content Extraction"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-2573: ADO Toolkit — LLM Vision Integration & Content Extraction

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that downloaded images are correctly passed to LLM vision model for content extraction.

## Preconditions

- ADO toolkit configured with `process_images: true`
- LLM vision model available and configured
- Image downloaded successfully from ADO
- LLM vision model has valid API credentials
- Network connectivity to LLM endpoint available

## Test Data

| Image Type | Content | Expected Output |
|-----------|---------|-----------------|
| Screenshot | UI elements, text | Text extracted |
| Diagram | Box, lines, labels | Structure described |
| Photograph | Objects, scene | Object/scene description |
| Chart | Data visualization | Data summary extracted |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_comments on work item with image in comment. | Tool downloads image; prepares for LLM analysis. |
| 2 | Verify downloaded image passed to LLM vision model. | LLM vision model receives image binary in correct format. |
| 3 | Verify LLM vision model endpoint called with proper authentication. | LLM API request succeeds (200 response); image processed. |
| 4 | Verify extracted text content returned from LLM. | Text description of image included in response. |
| 5 | Test with screenshot: verify UI elements and text extracted. | Relevant text and UI labels identified and returned. |
| 6 | Test with diagram: verify structure and relationships extracted. | Diagram structure, labels, and connections described. |
| 7 | Test with photograph: verify objects and scene described. | Object types, scene context, and relevant details extracted. |
| 8 | Test LLM failure scenario (API error). | Graceful error handling; processing continues; error logged. |
| 9 | Test empty/blank image: verify graceful handling. | Empty description returned or skipped; no blocking error. |

## Expected Final State

- Image passed to LLM vision model correctly
- LLM vision model successfully analyzes image
- Extracted text content included in response
- Multiple image types (screenshots, diagrams, photos) supported
- LLM failures handled gracefully
- Empty images handled without blocking

## Pass/Fail Criteria

**Pass:** Images passed to LLM; content extracted; multiple types supported; errors handled gracefully.  
**Fail:** Images not sent to LLM; LLM fails without graceful handling; content extraction fails; error blocks processing.
