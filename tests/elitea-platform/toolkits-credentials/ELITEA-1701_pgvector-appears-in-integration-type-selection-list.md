---
id: ELITEA-1701
title: Verify "PgVector" appears in the integration type selection list (Settings → New Integration)
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has permissions to create integrations
- User is on Settings → AI Configuration page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | AI Configuration page loads |
| 2 | Click "+ New Integration" button | "Select the integration Type" screen displays |
| 3 | Observe all available integration types | Multiple integration options are visible (AI DIAL, Amazon Bedrock, Azure OpenAI, Embedding model, LLM model, Ollama, OpenAI, PgVector, Speech Recognition, Text to Speech, Vertex AI) |
| 4 | Locate "PgVector" in the list | "PgVector" is clearly visible with a database/vector icon |
| 5 | Hover over PgVector option | Hover effect is displayed if applicable |

## Expected Final State

"PgVector" is prominently displayed in the integration type selection list with appropriate icon and styling.

## Pass/Fail Criteria

**Pass:**
- Integration type selection screen displays successfully
- "PgVector" (or "PGVector") is clearly visible
- PgVector has a distinct database/vector icon
- PgVector is positioned logically among other types
- Label is spelled correctly and matches UI conventions

**Fail:**
- PgVector is missing from the list
- PgVector label is misspelled or incorrectly formatted
- PgVector icon is missing or incorrect
- PgVector is not displayed with other integration types
