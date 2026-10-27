---
id: ELITEA-3791
title: "Configure Jira toolkit with base_url format variations and verify Check Connection"
priority: critical
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
- Valid Jira instance credentials (username and API token) are available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Jira base_url variant 1 | `https://jiraeu.epam.com` (no trailing slash) |
| Jira base_url variant 2 | `https://jiraeu.epam.com/` (single trailing slash) |
| Jira base_url variant 3 | `https://jiraeu.epam.com///` (multiple trailing slashes) |
| Jira username | Valid Jira username |
| Jira API token | Valid Jira API token |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" button and select "Jira" | New Jira Credential form opens |
| 3 | Enter Display Name: "Jira Test 1" | Display Name field accepts the input |
| 4 | Enter Base URL WITHOUT trailing slash: `https://jiraeu.epam.com` | Base URL field accepts the input |
| 5 | Select Auth type: "Bearer" and enter valid Jira token. Click "Check Connection" button | Success message displayed: "The connecton is OK!" |
| 6 | Click "Save" button | Credential saved successfully |
| 7 | Edit the same Jira credential | Credential form opens with saved values |
| 8 | Change Base URL to include single trailing slash: `https://jiraeu.epam.com/`. Click "Check Connection" button again | Success message displayed (URL normalized server-side, trailing slashes handled correctly) |
| 9 | Click "Save" button | Credential saved successfully |
| 10 | Edit the credential again | Credential form opens |
| 11 | Change Base URL to include multiple trailing slashes: `https://jiraeu.epam.com///`. Click "Check Connection" button | Success message displayed (URL normalized server-side, trailing slashes handled correctly) |
| 12 | Click "Save" button | Credential saved successfully with normalized URL |
| 13 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 214 | Click "+ Toolkit" button and select "Jira" | New Jira Toolkit form opens |
| 15 | Enter Toolkit Name: "Jira Toolkit Test" | Toolkit Name field accepts the input |
| 16 | In "Jira Configuration" dropdown, select the created credential "Jira Test 1" | Credential is selected successfully |
| 17 | Click "Save" button | Toolkit saved successfully and linked to the normalized credential |

## Expected Final State

- Jira credential is configured and saved successfully with normalized URL
- Jira toolkit is created and linked to the credential successfully
- All three URL format variations (no slash, single slash, multiple slashes) result in successful Check Connection at credential level
- URL normalization happens server-side transparently
- No error messages related to trailing slashes appear

## Pass/Fail Criteria

**Pass:**
- Jira credential accepts Base URL with and without trailing slashes
- Check Connection succeeds for all three URL format variations at credential level
- URL normalization removes trailing slashes before API client initialization
- No malformed URLs (double slashes) are generated in API endpoints
- Credential and toolkit save successfully in all cases
- Toolkit successfully references the normalized credential

**Fail:**
- Check Connection fails when Base URL has trailing slash(es)
- Error messages related to URL format appear
- Malformed URLs with double slashes are generated in API calls
- Credential fails to save with any URL format variation
- Toolkit cannot reference the credential
