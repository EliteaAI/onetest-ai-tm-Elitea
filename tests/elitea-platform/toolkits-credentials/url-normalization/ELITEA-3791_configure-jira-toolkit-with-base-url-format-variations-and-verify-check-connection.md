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
- User has access to Admin Panel > Toolkits section
- Valid Jira instance credentials are available

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
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Click "Add Toolkit" or "Configure Jira Toolkit" | Jira toolkit configuration form opens |
| 3 | Enter Jira base_url WITHOUT trailing slash: `https://jiraeu.epam.com` | URL field accepts the input |
| 4 | Enter valid Jira credentials (username, API token) | Credentials fields accept the input |
| 5 | Click "Check Connection" button | Connection check initiates, loading indicator displayed |
| 6 | Verify connection result | Success message displayed: "Connection successful" or similar |
| 7 | Save the toolkit configuration | Configuration saved successfully |
| 8 | Edit the same Jira toolkit configuration | Configuration form opens with saved values |
| 9 | Change base_url to include single trailing slash: `https://jiraeu.epam.com/` | URL field accepts the input with trailing slash |
| 10 | Click "Check Connection" button again | Connection check initiates |
| 11 | Verify connection result | Success message displayed (URL normalized, connection works same as without slash) |
| 12 | Edit the configuration again | Configuration form opens |
| 13 | Change base_url to include multiple trailing slashes: `https://jiraeu.epam.com///` | URL field accepts the input |
| 14 | Click "Check Connection" button | Connection check initiates |
| 15 | Verify connection result | Success message displayed (URL normalized, all trailing slashes removed) |
| 16 | Save the final configuration | Configuration saved successfully with normalized URL |

## Expected Final State

- Jira toolkit is configured and saved successfully
- All three URL format variations (no slash, single slash, multiple slashes) result in successful Check Connection
- URL normalization happens server-side transparently
- No error messages related to trailing slashes appear

## Pass/Fail Criteria

**Pass:**
- Jira toolkit accepts base_url with and without trailing slashes
- Check Connection succeeds for all three URL format variations
- URL normalization removes trailing slashes before client initialization
- No malformed URLs (double slashes) are generated
- Configuration saves successfully in all cases

**Fail:**
- Check Connection fails when base_url has trailing slash(es)
- Error messages related to URL format appear
- Malformed URLs with double slashes are generated
- Configuration fails to save with any URL format variation
