---
id: ELITEA-3803
title: "Verify Salesforce OAuth and REST API paths with normalized URL"
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
- Salesforce toolkit is configured with base_url containing trailing slash (e.g., `https://company.my.salesforce.com/`)
- Access to server logs or network inspection tools for URL verification

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Salesforce base_url | `https://company.my.salesforce.com/` (with trailing slash) |
| Salesforce credentials | Valid credentials |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure Salesforce toolkit with base_url containing trailing slash | Configuration accepted |
| 2 | Click "Check Connection" to initiate OAuth flow | OAuth process starts |
| 3 | Monitor network requests or server logs during OAuth | OAuth endpoints are properly formatted |
| 4 | Verify OAuth token endpoint URL | URL is normalized: `https://company.my.salesforce.com/services/oauth2/token` (no double slash) |
| 5 | Verify OAuth authorization endpoint URL | URL is normalized: `https://company.my.salesforce.com/services/oauth2/authorize` (no double slash) |
| 6 | Complete OAuth flow successfully | OAuth succeeds, access token obtained |
| 7 | Execute a Salesforce REST API call (e.g., query records) | API call executes |
| 8 | Monitor network requests during API call | REST API endpoint URLs are properly formatted |
| 9 | Verify REST API endpoint URL structure | URL is normalized: `https://company.my.salesforce.com/services/data/v57.0/query?q=...` (no double slash after base_url) |
| 10 | Execute multiple different API calls | All calls succeed |
| 11 | Verify all API endpoints use normalized base_url | No double slashes in any constructed URLs |

## Expected Final State

- OAuth authentication flow works correctly with normalized URL
- All OAuth endpoint URLs are properly formatted (no double slashes)
- REST API path construction uses normalized base_url
- All REST API endpoint URLs are valid and properly formatted
- Multiple API calls succeed without URL-related issues

## Pass/Fail Criteria

**Pass:**
- OAuth endpoints constructed correctly: `https://company.my.salesforce.com/services/oauth2/...` (not `https://company.my.salesforce.com//services/...`)
- REST API endpoints constructed correctly: `https://company.my.salesforce.com/services/data/...` (not `https://company.my.salesforce.com//services/...`)
- OAuth flow completes successfully
- All REST API calls return valid responses
- No malformed URLs detected in network traffic or logs

**Fail:**
- OAuth endpoint URLs contain double slashes
- REST API endpoint URLs contain double slashes
- OAuth authentication fails due to malformed URLs
- REST API calls fail due to URL formatting issues
- Any 400/404 errors related to URL structure
