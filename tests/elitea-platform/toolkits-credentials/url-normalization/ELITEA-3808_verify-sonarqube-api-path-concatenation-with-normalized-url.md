---
id: ELITEA-3808
title: "Verify SonarQube API path concatenation with normalized URL"
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
- SonarQube toolkit is configured with url containing trailing slash (e.g., `https://sonar.example.com/`)
- Access to server logs or network inspection tools for URL verification

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| SonarQube url | `https://sonar.example.com/` (with trailing slash) |
| Project key | Valid SonarQube project key |
| Relative API paths | `/api/measures/component`, `/api/issues/search`, `/api/projects/search` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure SonarQube toolkit with url containing trailing slash | Configuration accepted |
| 2 | Execute get_sonar_data tool with a specific project | Tool execution starts |
| 3 | Monitor network requests or server logs during execution | API calls are captured |
| 4 | Verify API endpoint URL for measures component | URL is normalized: `https://sonar.example.com/api/measures/component?...` (no double slash) |
| 5 | Execute another get_sonar_data call for different metric | Second API call made |
| 6 | Verify API endpoint URL structure | URL is normalized: `https://sonar.example.com/api/...` (not `https://sonar.example.com//api/...`) |
| 7 | Execute tool to search issues in SonarQube | Issues search API called |
| 8 | Verify issues search endpoint URL | URL properly formatted: `https://sonar.example.com/api/issues/search?...` |
| 9 | Execute tool to list projects | Projects list API called |
| 10 | Verify projects list endpoint URL | URL properly formatted: `https://sonar.example.com/api/projects/search?...` |
| 11 | Review all captured API calls | All URLs use normalized base (no double slashes) |

## Expected Final State

- All SonarQube API endpoints are constructed with normalized URL
- URL + relative path concatenation produces valid URLs without double slashes
- All API calls succeed and return valid data
- No malformed URLs in network traffic or logs

## Pass/Fail Criteria

**Pass:**
- All API endpoints constructed correctly: `https://sonar.example.com/api/...` (not `https://sonar.example.com//api/...`)
- URL normalization removes trailing slash before concatenating with relative paths
- get_sonar_data tool successfully concatenates base url with API paths
- All API calls return valid responses (200 OK)
- No URL-related errors in logs

**Fail:**
- API endpoint URLs contain double slashes
- URL concatenation produces malformed URLs
- API calls fail with 400/404 errors due to URL structure
- get_sonar_data fails to properly concatenate URL + path
- Trailing slash causes double slash in any API endpoint
