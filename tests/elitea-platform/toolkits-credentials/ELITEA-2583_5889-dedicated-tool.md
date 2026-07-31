---
id: ELITEA-2583
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Dedicated get_image_by_url Tool (Alternative)"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-2583: ADO Toolkit — Dedicated get_image_by_url Tool (Alternative Implementation)

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that dedicated `get_image_by_url` tool (if implemented as alternative) works correctly for explicit image processing on demand.

## Preconditions

- ADO toolkit available
- Dedicated `get_image_by_url` tool implemented (alternative to parameter approach)
- ADO credentials configured
- Image URLs accessible

## Test Data

| Input | Expected Output |
|-------|-----------------|
| Valid ADO image URL | Extracted text description |
| Invalid URL | Error message |
| Unauthorized URL | Permission error |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate `get_image_by_url` tool in ADO toolkit. | Tool is available and accessible. |
| 2 | Call tool with valid ADO image URL. | Tool accepts URL as input parameter. |
| 3 | Verify tool authenticates using ADO credentials from config. | Tool can access protected images. |
| 4 | Verify tool fetches image successfully. | Image downloaded (200 response). |
| 5 | Verify tool passes image to LLM vision model. | LLM vision model processes image. |
| 6 | Verify tool returns extracted text content. | Description returned as tool output. |
| 7 | Test with invalid URL. | Error message returned gracefully. |
| 8 | Test with unauthorized URL (403). | Permission error returned clearly. |
| 9 | Verify tool benefits from same caching as get_comments. | Duplicate URLs reuse cache. |
| 10 | Verify tool can be used independently from get_comments. | Explicit image processing on demand. |

## Expected Final State

- Dedicated tool accepts ADO image URL
- Authenticates with existing credentials
- Fetches and processes image
- Returns extracted text
- Handles errors gracefully
- Supports caching
- Can be used independently

## Pass/Fail Criteria

**Pass:** Tool working; URL accepted; auth correct; extraction successful; errors handled; caching works.  
**Fail:** Tool missing/broken; auth fails; extraction fails; errors not handled; caching broken.
