---
id: ELITEA-3730
title: "Verify notification text doesn't contain raw JSON"
priority: medium
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has notifications enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger indexing completion | Indexing completes |
| 2 | View notification | Notification is displayed |
| 3 | Inspect notification text | Text is human-readable |
| 4 | Verify no JSON formatting | No curly braces, quotes, or JSON structure visible |

## Expected Final State

Notification text is properly formatted prose, not raw JSON data.

## Pass/Fail Criteria

**Pass:**
- Notification is human-readable text
- Counts presented as sentences (e.g., "50 items indexed successfully")

**Fail:**
- Notification shows raw JSON (e.g., `{"indexed": 50}`)
- Technical formatting visible to end user
