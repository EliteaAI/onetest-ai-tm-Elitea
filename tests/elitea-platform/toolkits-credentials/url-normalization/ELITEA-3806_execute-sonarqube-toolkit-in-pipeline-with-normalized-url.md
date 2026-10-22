---
id: ELITEA-3806
title: "Execute SonarQube toolkit in Pipeline with normalized URL"
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
- SonarQube toolkit is configured with url containing trailing slash
- Check Connection for SonarQube toolkit passed successfully
- User has access to Pipelines section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| SonarQube url | `https://sonar.example.com/` (with trailing slash) |
| Pipeline name | `Test Pipeline - SonarQube URL Normalization` |
| Project key | Valid SonarQube project key |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section | Pipelines page loads successfully |
| 2 | Create pipeline or open existing pipeline | Pipeline editor opens |
| 3 | Add a SonarQube toolkit node to the pipeline | SonarQube toolkit node added |
| 4 | Configure the SonarQube node with get_sonar_data tool | Node configuration opens |
| 5 | Select the configured SonarQube toolkit (with trailing slash) | Toolkit selected |
| 6 | Configure tool parameters (project key, metrics) | Parameters set |
| 7 | Save the pipeline configuration | Pipeline saved successfully |
| 8 | Execute the pipeline | Pipeline execution starts |
| 9 | Observe pipeline execution | Pipeline progresses |
| 10 | Verify SonarQube node execution status | Node shows "Success" status |
| 11 | Check SonarQube node output | Output contains valid SonarQube data |
| 12 | Review execution logs | No URL-related errors |

## Expected Final State

- Pipeline executes successfully with SonarQube toolkit node
- SonarQube toolkit step completes without URL-related errors
- SonarQube API calls use properly normalized URLs
- Pipeline execution log shows successful SonarQube integration

## Pass/Fail Criteria

**Pass:**
- SonarQube toolkit node executes successfully
- Pipeline completes without errors
- SonarQube API calls return valid data
- No URL-related errors in logs
- API path concatenation works correctly

**Fail:**
- SonarQube node fails with URL-related errors
- Pipeline execution interrupted
- Malformed URLs generated
- API calls fail due to double slashes
