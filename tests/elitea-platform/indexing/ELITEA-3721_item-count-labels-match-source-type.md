---
id: ELITEA-3721
title: "Verify item count labels match source type"
priority: high
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has multiple toolkit types configured

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Source types | Jira (issues), Confluence (pages), GitHub (files), ADO (work items) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Index a Jira toolkit | Count label shows "issues" (not "files") |
| 2 | Index a Confluence toolkit | Count label shows "pages" (not "files") |
| 3 | Index a GitHub toolkit | Count label shows "files" |
| 4 | Index an ADO Work Items toolkit | Count label shows "work items" (not "files") |

## Expected Final State

Item count labels use terminology appropriate for each source type.

## Pass/Fail Criteria

**Pass:**
- Jira shows "issues indexed"
- Confluence shows "pages indexed"
- ADO shows "work items indexed"
- Labels match source type

**Fail:**
- All sources show generic "files indexed"
- Labels don't match the actual content type
