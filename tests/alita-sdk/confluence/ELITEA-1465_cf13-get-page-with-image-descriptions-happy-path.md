---
id: ELITEA-1465
title: "CF13 - Get Page with Image Descriptions (Happy Path)"
priority: critical
type: functional
module: confluence
status: ready
execution_type: automated
tags: [get_page_with_image_descriptions, confluence, images, pages, smoke]
requirements: []
---
# ELITEA-1465: CF13 - Get Page with Image Descriptions (Happy Path)

**Module:** Confluence · **Priority:** Critical · **Type:** Functional

**Objective:** Verify get_page_with_image_descriptions tool retrieves a page and replaces images with LLM-generated textual descriptions, returning augmented content as a string with the modified page text.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
Target page contains at least one image (CF_PAGE_WITH_IMAGES_ID)

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_PAGE_WITH_IMAGES_ID: ID of a Confluence page that contains at least one inline image

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_page_with_image_descriptions tool with ID of a page containing images (CF_PAGE_WITH_IMAGES_ID) | Augmented page content returned without errors |
| 2 | LLM validates: response is a string containing page content with image placeholders replaced by text descriptions, content is non-empty | Validation confirms get_page_with_image_descriptions processes images and returns augmented text content |

## Expected Final State

Validation confirms get_page_with_image_descriptions processes images and returns augmented text content

## Pass/Fail Criteria

PASS: Page content returned with image references replaced by textual descriptions, content is a non-empty string
FAIL: Tool crashes, returns page with unmodified image references, empty content
