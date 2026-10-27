---
id: ELITEA-3801
title: "Execute Salesforce toolkit in Pipeline with normalized URL"
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
- Salesforce toolkit is configured with base_url containing trailing slash
- Check Connection for Salesforce toolkit passed successfully
- User has access to Pipelines section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Salesforce base_url | `https://company.my.salesforce.com/` (with trailing slash) |
| Pipeline name | `Test Pipeline - Salesforce URL Normalization` |
| Salesforce object | Valid object name |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section | Pipelines page loads successfully |
| 2 | Create pipeline or open existing pipeline | Pipeline editor opens |
| 3 | Add a Salesforce toolkit node to the pipeline | Salesforce toolkit node added |
| 4 | Configure the Salesforce node with a tool (e.g., "Query records") | Node configuration opens |
| 5 | Select the configured Salesforce toolkit (with trailing slash) | Toolkit selected |
| 6 | Configure tool parameters (e.g., SOQL query) | Parameters set |
| 7 | Save the pipeline configuration | Pipeline saved successfully |
| 8 | Execute the pipeline | Pipeline execution starts |
| 9 | Observe pipeline execution | Pipeline progresses |
| 10 | Verify Salesforce node execution status | Node shows "Success" status |
| 11 | Check Salesforce node output | Output contains valid Salesforce data |
| 12 | Review execution logs | No URL-related errors |

## Expected Final State

- Pipeline executes successfully with Salesforce toolkit node
- Salesforce toolkit step completes without URL-related errors
- Salesforce REST API calls use properly normalized URLs
- Pipeline execution log shows successful Salesforce integration

## Pass/Fail Criteria

**Pass:**
- Salesforce toolkit node executes successfully
- Pipeline completes without errors
- Salesforce API calls return valid data
- No URL-related errors in logs
- OAuth and REST paths work correctly

**Fail:**
- Salesforce node fails with URL-related errors
- Pipeline execution interrupted
- Malformed URLs generated
- OAuth or REST API calls fail
