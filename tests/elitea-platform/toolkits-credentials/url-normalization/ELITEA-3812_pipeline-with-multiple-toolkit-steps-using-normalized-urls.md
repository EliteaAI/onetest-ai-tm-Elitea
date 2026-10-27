---
id: ELITEA-3812
title: "Pipeline with multiple toolkit steps (Jira, GitHub, Salesforce) using normalized URLs"
priority: high
type: integration
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, feat:pipelines, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Three toolkits configured with trailing slashes: Jira (`https://jiraeu.epam.com/`), GitHub (`https://github.example.com/api/v3/`), Salesforce (`https://company.my.salesforce.com/`)
- Check Connection passed for all three toolkits
- User has access to Pipelines section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Jira base_url | `https://jiraeu.epam.com/` (with trailing slash) |
| GitHub base_url | `https://github.example.com/api/v3/` (with trailing slash) |
| Salesforce base_url | `https://company.my.salesforce.com/` (with trailing slash) |
| Pipeline name | `Multi-Toolkit Pipeline - URL Normalization Test` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section | Pipelines page loads successfully |
| 2 | Create a new pipeline | Pipeline editor opens |
| 3 | Add Jira toolkit node as first step | Jira node added |
| 4 | Configure Jira node to search issues | Jira node configured (e.g., Search Issues tool) |
| 5 | Add GitHub toolkit node as second step | GitHub node added |
| 6 | Configure GitHub node to list repositories | GitHub node configured (e.g., List Repositories tool) |
| 7 | Add Salesforce toolkit node as third step | Salesforce node added |
| 8 | Configure Salesforce node to query records | Salesforce node configured (e.g., Query Records tool) |
| 9 | Save the pipeline configuration | Pipeline saved successfully |
| 10 | Execute the pipeline | Pipeline execution starts |
| 11 | Monitor Jira node execution | Jira node completes successfully (normalized URL used) |
| 12 | Verify Jira node output | Valid Jira data in output |
| 13 | Monitor GitHub node execution | GitHub node completes successfully (normalized URL used) |
| 14 | Verify GitHub node output | Valid GitHub data in output |
| 15 | Monitor Salesforce node execution | Salesforce node completes successfully (normalized URL used) |
| 16 | Verify Salesforce node output | Valid Salesforce data in output |
| 17 | Check overall pipeline status | Pipeline shows "Success" status |
| 18 | Review execution logs for all three nodes | No URL-related errors in any node |

## Expected Final State

- Pipeline executes successfully with all three toolkit nodes
- Each toolkit (Jira, GitHub, Salesforce) works correctly with normalized URLs
- All nodes complete without URL-related errors
- Pipeline execution log shows successful integration across all toolkits

## Pass/Fail Criteria

**Pass:**
- All three toolkit nodes execute successfully
- Pipeline completes end-to-end without errors
- Each toolkit returns valid data
- No URL-related errors in any node execution
- All API calls use properly normalized URLs
- Pipeline transitions smoothly between toolkit nodes

**Fail:**
- Any toolkit node fails with URL-related errors
- Pipeline execution interrupted at any node
- Malformed URLs generated in any toolkit call
- Any node shows error status
- Pipeline fails to complete
