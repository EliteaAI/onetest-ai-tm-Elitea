---
id: ELITEA-3804
title: "Configure SonarQube toolkit with url field format variations and verify Check Connection"
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
- Valid SonarQube instance credentials are available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| SonarQube url variant 1 | `https://sonar.example.com` (no trailing slash) |
| SonarQube url variant 2 | `https://sonar.example.com/` (single trailing slash) |
| SonarQube url variant 3 | `https://sonar.example.com///` (multiple trailing slashes) |
| SonarQube token | Valid SonarQube authentication token |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Click "Add Toolkit" or "Configure SonarQube Toolkit" | SonarQube toolkit configuration form opens |
| 3 | Enter SonarQube url WITHOUT trailing slash: `https://sonar.example.com` | URL field accepts the input |
| 4 | Enter valid SonarQube token | Token field accepts the input |
| 5 | Click "Check Connection" button | Connection check initiates, loading indicator displayed |
| 6 | Verify connection result | Success message displayed |
| 7 | Save the toolkit configuration | Configuration saved successfully |
| 8 | Edit the same SonarQube toolkit configuration | Configuration form opens with saved values |
| 9 | Change url to include single trailing slash: `https://sonar.example.com/` | URL field accepts the input with trailing slash |
| 10 | Click "Check Connection" button again | Connection check initiates |
| 11 | Verify connection result | Success message displayed (URL normalized) |
| 12 | Edit the configuration again | Configuration form opens |
| 13 | Change url to include multiple trailing slashes: `https://sonar.example.com///` | URL field accepts the input |
| 14 | Click "Check Connection" button | Connection check initiates |
| 15 | Verify connection result | Success message displayed (URL normalized, all trailing slashes removed) |
| 16 | Save the final configuration | Configuration saved successfully with normalized URL |

## Expected Final State

- SonarQube toolkit is configured and saved successfully
- All three URL format variations result in successful Check Connection
- URL normalization happens before API path concatenation
- No error messages related to trailing slashes or malformed URLs

## Pass/Fail Criteria

**Pass:**
- SonarQube toolkit accepts url with and without trailing slashes
- Check Connection succeeds for all three URL format variations
- URL normalization removes trailing slashes before use in get_sonar_data
- No malformed URLs (double slashes) are generated
- Configuration saves successfully in all cases

**Fail:**
- Check Connection fails when url has trailing slash(es)
- Error messages related to URL format appear
- Malformed API URLs with double slashes are generated
- Configuration fails to save with any URL format variation
