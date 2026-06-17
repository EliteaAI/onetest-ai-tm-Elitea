---
id: ELITEA-0984
title: "Tag API Functionality with Entity Coverage Parameter"
priority: high
type: functional
module: search-and-tag-filtering
status: draft
execution_type: manual
tags: [feat:pipelines, issue:2145, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2145]
---
# ELITEA-0984: Tag API Functionality with Entity Coverage Parameter

**Module:** Search And Tag Filtering · **Priority:** High · **Type:** Functional

**Objective:** Verify that the tag API correctly handles the entity_coverage parameter for context-aware tag filtering.

**Coverage:**
- API endpoint functionality with entity_coverage parameter
- Correct parameter processing and response formatting
- Tag data accuracy for specified entity types
- API response structure and data integrity

## Preconditions

- User logged into ELITEA platform
- Browser developer tools available
- API endpoints accessible for monitoring

## Test Data

- API endpoint: /api/v2/elitea_core/tags/prompt_lib/13
- Parameter combinations: entity_coverage=pipeline, entity_coverage=agent
- Test project ID: 13

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open browser developer tools and monitor Network tab | Network monitoring is active |
| 2 | Navigate to Pipeline page and perform tag search | API request triggered with entity_coverage=pipeline |
| 3 | Verify API response contains pipeline-specific tags | Response data shows tags relevant to pipelines |
| 4 | Navigate to Agent page and perform tag search | API request triggered with entity_coverage=agent |
| 5 | Verify API response contains agent-specific tags | Response data shows tags relevant to agents |
| 6 | Check API response format and data structure | Response follows expected JSON format with complete tag data |

## Expected Final State

Response follows expected JSON format with complete tag data

## Pass/Fail Criteria

**Pass:**
- API correctly processes entity_coverage parameter
- Returns appropriate tags based on entity type
- Response format and data structure are correct

**Fail:**
- API ignores or incorrectly processes entity_coverage parameter
- Returns wrong tags for specified entity type
- Response format is malformed or incomplete
