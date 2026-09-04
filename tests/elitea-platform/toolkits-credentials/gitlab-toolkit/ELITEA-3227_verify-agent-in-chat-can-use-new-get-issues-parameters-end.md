---
id: ELITEA-3227
title: "Verify agent in Chat can use new get_issues parameters end-to-end"
priority: high
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- Agent configured with the GitLab toolkit, `get_issues` tool enabled, added to a Chat conversation
- Test repository has 100+ matching issues for the truncation-check scenario
- (Optional) A Pipeline with a GitLab toolkit node available

## Test Data

| Field | Value |
|-------|-------|
| Prompt 1 | "Show me all closed issues in this repository" |
| Prompt 2 | "Show me issues labeled bug from the last 30 days" |
| Prompt 3 | "list all issues, including closed ones" (repo with 100+ matching issues) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the prompt "Show me all closed issues in this repository" | The agent invokes `get_issues` with `state=closed` and presents a correct, non-truncated list |
| 2 | Send the prompt "Show me issues labeled bug from the last 30 days" | The agent maps this to `labels`/`created_after` and returns a filtered result |
| 3 | Send a prompt requesting more than 20 issues (e.g. "list all issues, including closed ones") in a repo with 100+ matching issues | The agent either uses `fetch_all`/pagination to retrieve the full set or clearly indicates partial results, rather than silently truncating at ~20 as before the fix |
| 4 | If a Pipeline toolkit node is available, repeat with the node calling `get_issues` with explicit `state`/pagination/filter inputs | The node output reflects the filtered/paginated result correctly |

## Expected Final State

An agent in Chat correctly maps natural-language requests to the new `get_issues` parameters and presents accurate, non-silently-truncated results; a Pipeline node using the same parameters produces correct output.

## Pass/Fail Criteria

**Pass:**
- Natural-language prompts correctly map to `state`/`labels`/`created_after` parameters
- Large result sets are either fully retrieved or clearly flagged as partial, not silently truncated
- Pipeline node output matches the expected filtered/paginated result

**Fail:**
- The agent fails to invoke `get_issues` with the correct parameters for a clear natural-language request
- Results are silently truncated at ~20 with no indication
- Pipeline node output does not reflect the requested filters/pagination
