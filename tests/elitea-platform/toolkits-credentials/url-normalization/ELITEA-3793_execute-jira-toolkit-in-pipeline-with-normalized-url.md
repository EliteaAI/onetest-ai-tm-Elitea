---
id: ELITEA-3793
title: "Execute Jira toolkit in Pipeline with normalized URL"
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
- Jira toolkit is configured with base_url containing trailing slash (e.g., `https://jiraeu.epam.com/`)
- Check Connection for Jira toolkit passed successfully
- User has access to Pipelines section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Jira base_url | `https://jiraeu.epam.com/` (with trailing slash) |
| Pipeline name | `Test Pipeline - Jira URL Normalization` |
| Jira project key | Valid project key |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section | Pipelines page loads successfully |
| 2 | Click "Create Pipeline" or open existing pipeline | Pipeline editor opens |
| 3 | Add a Jira toolkit node/step to the pipeline | Jira toolkit node is added to pipeline canvas |
| 4 | Configure the Jira node with a tool (e.g., "Search Issues" or "Create Issue") | Node configuration opens |
| 5 | Select the configured Jira toolkit (with trailing slash in base_url) | Toolkit is selected from dropdown |
| 6 | Configure tool parameters (e.g., project key, search query) | Parameters are set |
| 7 | Save the pipeline configuration | Pipeline saved successfully |
| 8 | Execute the pipeline (Run/Test) | Pipeline execution starts |
| 9 | Observe pipeline execution progress | Pipeline progresses through nodes |
| 10 | Verify Jira node execution status | Jira node shows "Success" or "Completed" status |
| 11 | Check Jira node output/response | Node output contains valid Jira data |
| 12 | Review execution logs for any URL-related errors | No errors related to malformed URLs or client initialization |

## Expected Final State

- Pipeline executes successfully with Jira toolkit node
- Jira toolkit step completes without URL-related errors
- Jira API calls are made with properly normalized URLs
- Pipeline execution log shows successful Jira integration

## Pass/Fail Criteria

**Pass:**
- Jira toolkit node executes successfully in pipeline
- Pipeline completes without errors
- Jira API calls return valid data
- No URL-related errors in execution logs
- Jira client initializes correctly despite base_url having trailing slash

**Fail:**
- Jira toolkit node fails with URL-related errors
- Pipeline execution is interrupted
- Malformed URLs are generated (double slashes)
- Jira client initialization fails due to trailing slash
