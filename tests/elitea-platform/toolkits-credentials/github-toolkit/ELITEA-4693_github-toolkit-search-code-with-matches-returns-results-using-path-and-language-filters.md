---
id: ELITEA-4693
title: "GitHub Toolkit — search_code with matches returns results when using path: and language: filters"
priority: high
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [bug:7551, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7551"]
---
# ELITEA-4693: GitHub Toolkit — search_code with matches returns results when using path: and language: filters

**Module:** Github Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the #7551 fix, `search_code` still returns real results when the query matches code, including queries with `path:` and `language:` filters.

**Coverage:**
- `path:` filter
- `language:` filter
- Fields returned for each result

## Preconditions
- Logged in to `{{base_url}}` as a project member
- An agent with a GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `search_code` turned on
- The repo has workflow files under `.github/workflows/` that use `workflow_dispatch` (`main.yml`, `test-workflow.yml`, `runs-test-data.yml`)
- The repo has Python files containing `def` (`idd.py`, `main.py`, `script.py`)

## Test Data
| Field | Value |
|-------|-------|
| Query 1 | `workflow_dispatch path:.github` |
| Query 2 | `def language:python` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent, select the `search_code` tool and run it with Query 1. | The tool succeeds and returns `total_count: 3` with `.github/workflows/main.yml`, `test-workflow.yml` and `runs-test-data.yml` in `items`. |
| 2 | Check one item from step 1. | It has `name`, `path`, `sha`, `html_url` and repository details. `html_url` opens the file on GitHub. |
| 3 | Run `search_code` with Query 2. | The tool succeeds and returns `total_count: 3` with `idd.py`, `main.py` and `script.py` in `items`. |
| 4 | Check that only files from `SamvelSimonyan/testRepo` are returned. | Every item's repository is `SamvelSimonyan/testRepo`. |

## Expected Final State
Both searches return the matching files from the toolkit's repo with full result details and no errors.

## Pass/Fail Criteria

**Pass:**
- Both queries return the expected files with `name`, `path`, `sha` and `html_url`, all from `SamvelSimonyan/testRepo`

**Fail:**
- Either query returns an error, a "No code found" message, or files from another repo
