---
id: ELITEA-3795
title: "Configure GitHub toolkit with base_url format variations and verify Check Connection"
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
- Valid GitHub Enterprise or GitHub.com credentials are available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| GitHub base_url variant 1 | `https://github.example.com/api/v3` (no trailing slash) |
| GitHub base_url variant 2 | `https://github.example.com/api/v3/` (single trailing slash) |
| GitHub base_url variant 3 | `https://github.example.com/api/v3///` (multiple trailing slashes) |
| GitHub token | Valid GitHub personal access token or App credentials |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Click "Add Toolkit" or "Configure GitHub Toolkit" | GitHub toolkit configuration form opens |
| 3 | Enter GitHub base_url WITHOUT trailing slash: `https://github.example.com/api/v3` | URL field accepts the input |
| 4 | Enter valid GitHub credentials (token or App credentials) | Credentials fields accept the input |
| 5 | Click "Check Connection" button | Connection check initiates, loading indicator displayed |
| 6 | Verify connection result | Success message displayed |
| 7 | Save the toolkit configuration | Configuration saved successfully |
| 8 | Edit the same GitHub toolkit configuration | Configuration form opens with saved values |
| 9 | Change base_url to include single trailing slash: `https://github.example.com/api/v3/` | URL field accepts the input with trailing slash |
| 10 | Click "Check Connection" button again | Connection check initiates |
| 11 | Verify connection result | Success message displayed (URL normalized) |
| 12 | Edit the configuration again | Configuration form opens |
| 13 | Change base_url to include multiple trailing slashes: `https://github.example.com/api/v3///` | URL field accepts the input |
| 14 | Click "Check Connection" button | Connection check initiates |
| 15 | Verify connection result | Success message displayed (URL normalized, all trailing slashes removed) |
| 16 | Save the final configuration | Configuration saved successfully with normalized URL |

## Expected Final State

- GitHub toolkit is configured and saved successfully
- All three URL format variations result in successful Check Connection
- URL normalization happens server-side transparently
- No error messages related to trailing slashes or malformed URLs

## Pass/Fail Criteria

**Pass:**
- GitHub toolkit accepts base_url with and without trailing slashes
- Check Connection succeeds for all three URL format variations
- URL normalization removes trailing slashes before API endpoint construction
- No malformed URLs (double slashes) are generated
- Configuration saves successfully in all cases

**Fail:**
- Check Connection fails when base_url has trailing slash(es)
- Error messages related to URL format appear
- Malformed API endpoint URLs with double slashes are generated
- Configuration fails to save with any URL format variation
