---
id: ELITEA-4694
title: "Regression - GitHub Toolkit search_code returns results or a \"No code found\" message without errors"
priority: critical
type: regression
module: github-toolkit
status: draft
execution_type: manual
tags: [bug:7551, feat:toolkits, r-2.0.9, automated:UI:regression]
requirements: ["EliteaAI/elitea_issues#7551"]
---
# ELITEA-4694: Regression - GitHub Toolkit search_code returns results or a "No code found" message without errors

**Module:** Github Toolkit · **Priority:** Critical · **Type:** Regression

**Objective:** Verify in the GitHub toolkit's Test Settings panel that `search_code` returns a clean "No code found" result when nothing matches (#7551), and still returns matching files when the query matches code.

Manual source: ELITEA-4692, ELITEA-4693

**Coverage:**
- No-match queries return an empty result with a "No code found" message, not a tool error
- A query that matches code returns the matching files with full result fields
- The toolkit's default repo is added to the query as `repo:`

## Preconditions
- Logged in to `{{base_url}}` as a project member
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `search_code` turned on (create it through the API in setup)
- The repo has no code containing `zzqx_nonexistent_string_7551`
- The repo has workflow files `.github/workflows/main.yml`, `test-workflow.yml` and `runs-test-data.yml` that use `workflow_dispatch`

## Test Data
| Field | Value |
|-------|-------|
| No-match query 1 | `429` |
| No-match query 2 | `zzqx_nonexistent_string_7551` |
| Match query | `workflow_dispatch path:.github` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to its Test Settings panel and select the `search_code` tool. | The `query` field is shown. |
| 2 | Enter No-match query 1 and run the tool. | The run succeeds. The output has `total_count: 0`, `items: []` and the message `No code found for query '429 repo:SamvelSimonyan/testRepo'.` |
| 3 | Enter No-match query 2 and run the tool. | The run succeeds. The output has `total_count: 0`, `items: []` and a "No code found" message containing `zzqx_nonexistent_string_7551 repo:SamvelSimonyan/testRepo`. |
| 4 | Enter the Match query and run the tool. | The run succeeds. The output has `total_count: 3` and `items` lists `main.yml`, `test-workflow.yml` and `runs-test-data.yml`. |
| 5 | Check the items from step 4. | Each item has `name`, `path`, `sha` and `html_url`, and its repository is `SamvelSimonyan/testRepo`. |
| 6 | Check the output of all three runs. | No run shows a tool execution error or a GitHub API error. |

## Expected Final State
No-match queries return a clean "No code found" result and the match query returns the 3 workflow files. No run shows an error.

## Pass/Fail Criteria

**Pass:**
- Steps 2–3 return `total_count: 0`, empty `items` and a "No code found" message with the default `repo:` filter
- Step 4 returns the 3 expected files with full result fields, all from `SamvelSimonyan/testRepo`

**Fail:**
- Any run returns a tool execution error, or the match query returns no results or files from another repo
