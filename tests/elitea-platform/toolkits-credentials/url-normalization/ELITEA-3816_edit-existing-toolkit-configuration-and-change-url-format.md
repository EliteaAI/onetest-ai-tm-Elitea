---
id: ELITEA-3816
title: "Edit existing toolkit configuration and change URL format"
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
- User has access to Admin Panel > Toolkits section
- Four toolkits are pre-configured: Jira, GitHub, Salesforce, SonarQube (all with URLs WITHOUT trailing slashes)

## Test Data

| Toolkit Type | Original URL (no slash) | Modified URL (with slash) |
|--------------|------------------------|---------------------------|
| Jira | `https://jiraeu.epam.com` | `https://jiraeu.epam.com/` |
| GitHub | `https://github.example.com/api/v3` | `https://github.example.com/api/v3/` |
| Salesforce | `https://company.my.salesforce.com` | `https://company.my.salesforce.com/` |
| SonarQube | `https://sonar.example.com` | `https://sonar.example.com/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Locate pre-configured Jira toolkit in list | Jira toolkit visible |
| 3 | Click "Edit" or open Jira toolkit configuration | Configuration form opens with saved values |
| 4 | Verify current base_url: `https://jiraeu.epam.com` (no trailing slash) | URL displayed without trailing slash |
| 5 | Edit base_url to add trailing slash: `https://jiraeu.epam.com/` | Field accepts the change |
| 6 | Click "Check Connection" to verify | Connection check initiates |
| 7 | Verify connection succeeds with new URL format | Success message displayed (URL normalized) |
| 8 | Click "Save" to update configuration | Configuration updated successfully |
| 9 | Close and reopen Jira toolkit configuration | Configuration opens with updated URL |
| 10 | Verify Jira toolkit still works (execute a test tool call) | Toolkit functions correctly with normalized URL |
| 11 | Repeat steps 2-10 for GitHub toolkit | GitHub toolkit updated and works correctly |
| 12 | Repeat steps 2-10 for Salesforce toolkit | Salesforce toolkit updated and works correctly |
| 13 | Repeat steps 2-10 for SonarQube toolkit | SonarQube toolkit updated and works correctly |
| 14 | Edit Jira toolkit again, change URL back to no trailing slash | URL change accepted |
| 15 | Save and verify Jira toolkit still works | Toolkit works correctly (URL remains unchanged by normalization since no trailing slash) |

## Expected Final State

- All four toolkits can be edited to change URL format (add/remove trailing slash)
- URL format changes are saved successfully
- Check Connection works correctly after URL format changes
- Toolkits continue to function normally after editing
- URL normalization is transparent during edit workflow

## Pass/Fail Criteria

**Pass:**
- All four toolkits can be edited successfully
- URL field accepts both formats (with and without trailing slash)
- Check Connection succeeds after URL format change
- Configuration saves successfully after URL edit
- Toolkits function correctly after URL format change
- Editing is repeatable (can change URL format multiple times)
- No data loss during edit operations

**Fail:**
- Unable to edit existing toolkit configuration
- URL format change rejected or causes errors
- Check Connection fails after adding trailing slash
- Configuration fails to save after URL edit
- Toolkit stops working after URL format change
- Data loss or corruption during edit
