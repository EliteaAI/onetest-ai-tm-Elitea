---
id: ELITEA-4692
title: "GitHub Toolkit — search_code with no matches returns a \"No code found\" result instead of an error"
priority: critical
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [bug:7551, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7551"]
---
# ELITEA-4692: GitHub Toolkit — search_code with no matches returns a "No code found" result instead of an error

**Module:** Github Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the fix for #7551: when `search_code` finds nothing, it returns an empty result with a clear "No code found" message, not a tool error.

**Coverage:**
- Plain keyword, exact phrase and a string that exists nowhere
- The toolkit's default repo is added to the query as `repo:` automatically

## Preconditions
- Logged in to `{{base_url}}` as a project member
- An agent with a GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `search_code` turned on
- The repo has no code containing `429`, `"package main"` or `zzqx_nonexistent_string_7551`

## Test Data
| Field | Value |
|-------|-------|
| Query 1 | `429` |
| Query 2 | `"package main"` |
| Query 3 | `zzqx_nonexistent_string_7551` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent, select the `search_code` tool and run it with Query 1. | The tool succeeds. The result has `total_count: 0`, `items: []` and the message `No code found for query '429 repo:SamvelSimonyan/testRepo'.` |
| 2 | Run `search_code` with Query 2. | The tool succeeds. The result has `total_count: 0`, `items: []` and a "No code found" message containing `"package main" repo:SamvelSimonyan/testRepo`. |
| 3 | Run `search_code` with Query 3. | The tool succeeds. The result has `total_count: 0`, `items: []` and a "No code found" message containing `zzqx_nonexistent_string_7551 repo:SamvelSimonyan/testRepo`. |
| 4 | Check the tool output panel for all three runs. | No run shows a tool execution error, a stack trace or a GitHub API error. |

## Expected Final State
All three searches finish without errors and each returns a clean empty result with a "No code found" message.

## Pass/Fail Criteria

**Pass:**
- Every query returns `total_count: 0`, an empty `items` list and a "No code found" message that shows the query with the default `repo:` filter

**Fail:**
- Any query returns a tool execution error or an error message instead of the empty result
