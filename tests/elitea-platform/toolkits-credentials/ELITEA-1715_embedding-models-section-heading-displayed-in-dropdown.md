---
id: ELITEA-1715
title: Verify "EMBEDDING MODELS" section heading is displayed in Embedding Model dropdown
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:embedding-models, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on agent/toolkit configuration page
- At least one embedding model is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent configuration page | Page loads |
| 2 | Expand "Toolkit" section | Section expands |
| 3 | Locate "Embedding Model" dropdown field | Field is visible |
| 4 | Click on the Embedding Model dropdown | Dropdown opens |
| 5 | Observe the section heading at the top of dropdown | "EMBEDDING MODELS" section heading appears in uppercase at the top; heading is clearly distinguishable from model list items below |

## Expected Final State

"EMBEDDING MODELS" heading is prominently displayed in the dropdown with consistent styling matching PGVector dropdown.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens successfully
- "EMBEDDING MODELS" heading appears in uppercase
- Heading is positioned at the top of dropdown
- Heading uses consistent font style, size, and color with "SAVED PGVECTOR CREDENTIALS"
- Heading is clearly distinguishable from model items
- Overall dropdown styling matches PGVector dropdown style

**Fail:**
- Heading is missing or incorrect
- Heading uses wrong casing or styling
- Heading doesn't match PGVector dropdown style
- Heading is positioned incorrectly
- Styling is inconsistent
