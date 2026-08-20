---
id: ELITEA-2655
title: "ADO Repos - search_code: query parameter (keyword, phrase, embedded scope syntax)"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-2655: ADO Repos - search_code: query parameter (keyword, phrase, embedded scope syntax)

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify the `query` parameter alone (no other parameters set) correctly finds matching code by keyword, exact phrase, and by scope syntax embedded directly in the query string (`ext:`, `path:`).

## Preconditions

- ADO Repos toolkit configured with valid credentials against a repository with known searchable content.
- Repository has at least one file under a known subfolder (e.g. `src/services`) and at least one file with a known extension (e.g. `.py`).

## Test Data

| `query` value | Expectation |
|---|---|
| `QueueJobsNow` | Matches on a known identifier present in the repo |
| `"exact phrase here"` | Matches only the exact phrase |
| `parse_response ext:py` | Only `.py` files returned |
| `retry path:src/services` | Only files under `src/services` returned |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with only `query="QueueJobsNow"`, all other params default | Matching result(s) returned for the known identifier |
| 2 | Call `search_code` with `query="\"exact phrase here\""` | Only exact-phrase matches returned |
| 3 | Call `search_code` with `query="parse_response ext:py"` | Only `.py` files returned |
| 4 | Call `search_code` with `query="retry path:src/services"` | Only files under `src/services` returned |

## Expected Final State

Every query variant returns results consistent with its expected scoping/matching behavior.

## Pass/Fail Criteria

**Pass:**
- Keyword query returns known matches
- Phrase query returns exact-phrase-only matches
- ext: and path: embedded in the query correctly scope results

**Fail:**
- Any query variant returns incorrect, unrelated, or no results when matches are known to exist
