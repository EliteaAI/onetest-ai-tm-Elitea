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
- User has access to Credentials and Toolkits & Indexes sections
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
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" button and select "Salesforce" | New Salesforce Credential form opens |
| 3 | Enter Display Name: "Salesforce Test 1" | Display Name field accepts the input |
| 4 | Enter ID (auto-generated or custom) | ID field accepts the input |
| 5 | Enter Base URL WITHOUT trailing slash: `https://company.my.salesforce.com` | Base URL field accepts the input |
| 6 | Select Auth type: "Bearer" (or appropriate Salesforce auth type) | Auth type is selected |
| 7 | Enter valid Salesforce credentials (username, password, security token) | Credentials fields accept the input |
| 8 | Click "Check Connection" button | Connection check initiates, loading indicator displayed |
| 9 | Verify connection result | Success message displayed |
| 10 | Click "Save" button | Credential saved successfully |
| 11 | Edit the same Salesforce credential | Credential form opens with saved values |
| 12 | Change Base URL to include single trailing slash: `https://company.my.salesforce.com/` | Base URL field accepts the input with trailing slash |
| 13 | Click "Check Connection" button again | Connection check initiates |
| 14 | Verify connection result | Success message displayed (URL normalized, OAuth works correctly) |
| 15 | Click "Save" button | Credential saved successfully |
| 16 | Edit the credential again | Credential form opens |
| 17 | Change Base URL to include multiple trailing slashes: `https://company.my.salesforce.com///` | Base URL field accepts the input |
| 18 | Click "Check Connection" button | Connection check initiates |
| 19 | Verify connection result | Success message displayed (URL normalized, all trailing slashes removed) |
| 20 | Click "Save" button | Credential saved successfully with normalized URL |
| 21 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 22 | Click "+ Toolkit" button and select "Salesforce" | New Salesforce Toolkit form opens |
| 23 | Enter Toolkit Name: "Salesforce Toolkit Test" | Toolkit Name field accepts the input |
| 24 | In "Salesforce Configuration" dropdown, select the created credential "Salesforce Test 1" | Credential is selected successfully |
| 25 | Click "Save" button | Toolkit saved successfully and linked to the normalized credential |

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
