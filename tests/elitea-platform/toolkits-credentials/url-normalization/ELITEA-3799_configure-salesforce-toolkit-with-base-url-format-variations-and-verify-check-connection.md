---
id: ELITEA-3799
title: "Configure Salesforce toolkit with base_url format variations and verify Check Connection"
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
- Valid Salesforce instance credentials are available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Salesforce base_url variant 1 | `https://company.my.salesforce.com` (no trailing slash) |
| Salesforce base_url variant 2 | `https://company.my.salesforce.com/` (single trailing slash) |
| Salesforce base_url variant 3 | `https://company.my.salesforce.com///` (multiple trailing slashes) |
| Salesforce username | Valid Salesforce username |
| Salesforce security token | Valid security token |
| Salesforce password | Valid password |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Click "Add Toolkit" or "Configure Salesforce Toolkit" | Salesforce toolkit configuration form opens |
| 3 | Enter Salesforce base_url WITHOUT trailing slash: `https://company.my.salesforce.com` | URL field accepts the input |
| 4 | Enter valid Salesforce credentials (username, password, security token) | Credentials fields accept the input |
| 5 | Click "Check Connection" button | Connection check initiates, loading indicator displayed |
| 6 | Verify connection result | Success message displayed |
| 7 | Save the toolkit configuration | Configuration saved successfully |
| 8 | Edit the same Salesforce toolkit configuration | Configuration form opens with saved values |
| 9 | Change base_url to include single trailing slash: `https://company.my.salesforce.com/` | URL field accepts the input with trailing slash |
| 10 | Click "Check Connection" button again | Connection check initiates |
| 11 | Verify connection result | Success message displayed (URL normalized, OAuth works correctly) |
| 12 | Edit the configuration again | Configuration form opens |
| 13 | Change base_url to include multiple trailing slashes: `https://company.my.salesforce.com///` | URL field accepts the input |
| 14 | Click "Check Connection" button | Connection check initiates |
| 15 | Verify connection result | Success message displayed (URL normalized, all trailing slashes removed) |
| 16 | Save the final configuration | Configuration saved successfully with normalized URL |

## Expected Final State

- Salesforce toolkit is configured and saved successfully
- All three URL format variations result in successful Check Connection
- URL normalization happens before OAuth flow and REST API path construction
- No error messages related to trailing slashes or malformed URLs

## Pass/Fail Criteria

**Pass:**
- Salesforce toolkit accepts base_url with and without trailing slashes
- Check Connection succeeds for all three URL format variations
- OAuth authentication flow works correctly with normalized URL
- REST API paths are constructed properly (no double slashes)
- Configuration saves successfully in all cases

**Fail:**
- Check Connection fails when base_url has trailing slash(es)
- OAuth authentication fails due to URL format issues
- Error messages related to URL format appear
- Malformed REST API URLs with double slashes are generated
- Configuration fails to save with any URL format variation
