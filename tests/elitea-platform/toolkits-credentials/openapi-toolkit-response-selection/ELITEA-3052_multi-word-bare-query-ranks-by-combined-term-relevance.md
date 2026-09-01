---
id: ELITEA-3052
title: "Multi-Word Bare Query Ranks Items by Combined-Term BM25 Relevance"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3052: Multi-Word Bare Query Ranks Items by Combined-Term BM25 Relevance

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a multi-word bare query (no quotes/exclusions, e.g. `active enterprise`) contributes both terms to relevance — items matching both terms rank above items matching only one, which rank above items matching neither. Confirmed live during the follow-up P0/P1 checklist pass ("multi-word bare query relevance").

---

## Preconditions

- An OpenAPI toolkit configured against an operation whose response contains items with varying overlap against two chosen terms (some items match both, some match one, some match neither).

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | `active enterprise` (or equivalent two-term query for the dataset in use) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with the two-term query. | Call succeeds. |
| 2 | Inspect the ranked order of returned items. | Items matching both terms appear before items matching only one term, which appear before (or are excluded ahead of) items matching neither. |

---

## Expected Final State

BM25 scoring correctly aggregates relevance across multiple query terms.

---

## Pass/Fail Criteria

**Pass:** Ranking order reflects combined-term relevance as described.
**Fail:** Ranking ignores one of the terms, or items matching fewer terms outrank items matching more terms.
