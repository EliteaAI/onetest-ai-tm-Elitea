---
id: ELITEA-3816
title: "Edit existing credential configuration and change URL format"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to Credentials and Toolkits & Indexes sections
- Four credentials are pre-configured: Jira, GitHub, Salesforce, SonarQube (all with Base URLs WITHOUT trailing slashes)

## Test Data

| Credential Type | Original URL (no slash) | Modified URL (with slash) |
|-----------------|------------------------|---------------------------|
| Jira | `https://jira.example.com` | `https://jira.example.com/` |
| GitHub | `https://github.example.com/api/v3` | `https://github.example.com/api/v3/` |
| Salesforce | `https://company.my.salesforce.com` | `https://company.my.salesforce.com/` |
| SonarQube | `https://sonar.example.com` | `https://sonar.example.com/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Locate pre-configured Jira credential in list | Jira credential visible |
| 3 | Click "Edit" or open Jira credential configuration | Credential form opens with saved values |
| 4 | Verify current Base URL: `https://jira.example.com` (no trailing slash) | URL displayed without trailing slash |
| 5 | Edit Base URL to add trailing slash: `https://jira.example.com/` | Field accepts the change |
| 6 | Click "Check Connection" to verify | Connection check initiates |
| 7 | Verify connection succeeds with new URL format | Success message displayed (URL normalized) |
| 8 | Click "Save" to update credential | Credential updated successfully |
| 9 | Close and reopen Jira credential configuration | Credential opens with updated URL |
| 10 | Navigate to Toolkits and verify linked Jira toolkit still works | Toolkit references updated credential correctly |
| 11 | Repeat steps 2-10 for GitHub credential | GitHub credential updated and linked toolkit works correctly |
| 12 | Repeat steps 2-10 for Salesforce credential | Salesforce credential updated and linked toolkit works correctly |
| 13 | Repeat steps 2-10 for SonarQube credential | SonarQube credential updated and linked toolkit works correctly |
| 14 | Edit Jira credential again, change URL back to no trailing slash | URL change accepted |
| 15 | Save and verify linked Jira toolkit still works | Toolkit works correctly (URL remains unchanged by normalization since no trailing slash) |

## Expected Final State

- All four credentials can be edited to change URL format (add/remove trailing slash)
- URL format changes are saved successfully
- Check Connection works correctly after URL format changes
- Linked toolkits continue to function normally after credential editing
- URL normalization is transparent during edit workflow

## Pass/Fail Criteria

**Pass:**
- All four credentials can be edited successfully
- Base URL field accepts both formats (with and without trailing slash)
- Check Connection succeeds after URL format change
- Credential saves successfully after URL edit
- Linked toolkits function correctly after credential URL format change
- Editing is repeatable (can change URL format multiple times)
- No data loss during edit operations

**Fail:**
- Unable to edit existing credential configuration
- URL format change rejected or causes errors
- Check Connection fails after adding trailing slash
- Configuration fails to save after URL edit
- Toolkit stops working after URL format change
- Data loss or corruption during edit
