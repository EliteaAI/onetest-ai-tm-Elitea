---
id: ELITEA-3814
title: "Toolkit configuration error handling with invalid URL formats"
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

## Test Data

| Test Scenario | Input URL | Expected Behavior |
|---------------|-----------|-------------------|
| Invalid URL (not a URL) | `not-a-url` | Validation error: "Invalid URL format" |
| Missing protocol | `jiraeu.epam.com/` | Validation error or warning |
| URL with spaces | `https://jira eu.epam.com/` | Validation error: "URL contains invalid characters" |
| Very long URL with trailing slash | `https://very-long-subdomain-name-that-exceeds-normal-length.example.com/` | URL normalized, connection attempt (may fail for other reasons, not URL format) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Start configuring a Jira toolkit | Configuration form opens |
| 3 | Enter invalid URL (not a URL): `not-a-url` | Field validation triggers |
| 4 | Attempt to save or check connection | Appropriate error message displayed: "Invalid URL format" or similar |
| 5 | Clear field and enter URL without protocol: `jiraeu.epam.com/` | Field validation triggers or warning shown |
| 6 | Attempt to check connection | Appropriate error or warning about missing protocol |
| 7 | Clear field and enter URL with spaces: `https://jira eu.epam.com/` | Field validation triggers |
| 8 | Attempt to save configuration | Error message: "URL contains invalid characters" or similar |
| 9 | Clear field and enter very long valid URL with trailing slash: `https://very-long-subdomain-name-that-exceeds-normal-length.example.com/` | URL accepted, field validation passes |
| 10 | Click "Check Connection" | URL is normalized (trailing slash removed), connection attempt made |
| 11 | Verify error message does NOT mention trailing slash issue | If connection fails, error is about unreachable host or credentials, NOT URL format |
| 12 | Configure toolkit with valid URL + wrong credentials + trailing slash | URL normalized, credentials fail |
| 13 | Verify error message mentions credentials, not URL format | Error: "Invalid credentials" or "Authentication failed", NOT URL format error |

## Expected Final State

- Invalid URL formats are properly validated and rejected
- Error messages clearly indicate the actual issue (invalid format, missing protocol, etc.)
- Trailing slash issue does NOT appear in error messages after normalization implementation
- Valid URLs with trailing slashes are normalized and accepted

## Pass/Fail Criteria

**Pass:**
- Invalid URL formats trigger appropriate validation errors
- Error messages accurately describe the issue
- URL normalization handles valid URLs with trailing slashes silently
- Error messages do NOT incorrectly suggest trailing slash as problem when issue is elsewhere (credentials, network, etc.)
- Very long valid URLs with trailing slashes are accepted and normalized
- URL validation is independent of trailing slash handling

**Fail:**
- Invalid URLs are accepted without validation
- Error messages are unclear or misleading
- Valid URLs with trailing slashes trigger format errors
- Error messages incorrectly blame trailing slash for other issues (credentials, network)
- URL validation crashes or behaves unexpectedly
