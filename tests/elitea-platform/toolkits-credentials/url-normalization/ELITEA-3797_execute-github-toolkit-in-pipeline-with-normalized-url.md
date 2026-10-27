---
id: ELITEA-3797
title: "Execute GitHub toolkit in Pipeline with normalized URL"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, feat:pipelines, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- GitHub toolkit is configured with base_url containing trailing slash
- Check Connection for GitHub toolkit passed successfully
- User has access to Pipelines section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| GitHub base_url | `https://api.github.com/` (with trailing slash) |
| Pipeline name | `Test Pipeline - GitHub URL Normalization` |
| Repository | Valid repository name |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section | Pipelines page loads successfully |
| 2 | Create pipeline or open existing pipeline | Pipeline editor opens |
| 3 | Add a GitHub toolkit node to the pipeline | GitHub toolkit node added |
| 4 | Configure the GitHub node with a tool (e.g., "List files", "Get repository") | Node configuration opens |
| 5 | Select the configured GitHub toolkit (with trailing slash) | Toolkit selected |
| 6 | Configure tool parameters | Parameters set |
| 7 | Save the pipeline configuration | Pipeline saved successfully |
| 8 | Execute the pipeline | Pipeline execution starts |
| 9 | Observe pipeline execution | Pipeline progresses |
| 10 | Verify GitHub node execution status | Node shows "Success" status |
| 11 | Check GitHub node output | Output contains valid GitHub data |
| 12 | Review execution logs | No URL-related errors |

## Expected Final State

- Pipeline executes successfully with GitHub toolkit node
- GitHub toolkit step completes without URL-related errors
- GitHub API calls use properly normalized URLs
- Pipeline execution log shows successful GitHub integration

## Pass/Fail Criteria

**Pass:**
- GitHub toolkit node executes successfully
- Pipeline completes without errors
- GitHub API calls return valid data
- No URL-related errors in logs
- GitHub client initializes correctly

**Fail:**
- GitHub node fails with URL-related errors
- Pipeline execution interrupted
- Malformed URLs generated
- GitHub client initialization fails
