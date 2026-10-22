---
id: ELITEA-3809
title: "URL normalization function unit test with edge cases"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User has access to codebase or test environment where URL normalization function can be tested
- URL normalization function is implemented and available

## Test Data

| Test Scenario | Input URL | Expected Output |
|---------------|-----------|-----------------|
| No trailing slash | `https://example.com` | `https://example.com` (unchanged) |
| Single trailing slash | `https://example.com/` | `https://example.com` (slash removed) |
| Multiple trailing slashes | `https://example.com///` | `https://example.com` (all slashes removed) |
| Empty string | `` (empty) | `` or appropriate error/None |
| Null/None value | `null` or `None` | Appropriate error or None |
| URL with query params | `https://example.com/path?key=value` | `https://example.com/path?key=value` (unchanged, no trailing slash) |
| URL with query params and trailing slash | `https://example.com/path/?key=value` | `https://example.com/path?key=value` (slash before ? removed) |
| URL with path and trailing slash | `https://example.com/api/v3/` | `https://example.com/api/v3` (slash removed) |
| URL with port | `https://example.com:8080/` | `https://example.com:8080` (slash removed) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call URL normalization function with URL without trailing slash: `https://example.com` | Function returns same URL unchanged: `https://example.com` |
| 2 | Call function with URL with single trailing slash: `https://example.com/` | Function returns URL without slash: `https://example.com` |
| 3 | Call function with URL with multiple trailing slashes: `https://example.com///` | Function returns URL with all slashes removed: `https://example.com` |
| 4 | Call function with empty string: `` | Function handles gracefully (returns empty string or raises appropriate error) |
| 5 | Call function with null/None value | Function handles gracefully (returns None or raises appropriate error) |
| 6 | Call function with URL containing query parameters: `https://example.com/path?key=value` | Function returns URL unchanged (query params preserved) |
| 7 | Call function with URL with query params and trailing slash before ?: `https://example.com/path/?key=value` | Function removes trailing slash: `https://example.com/path?key=value` |
| 8 | Call function with URL with path: `https://example.com/api/v3/` | Function removes trailing slash: `https://example.com/api/v3` |
| 9 | Call function with URL with port and trailing slash: `https://example.com:8080/` | Function removes trailing slash: `https://example.com:8080` |
| 10 | Verify function is idempotent (calling twice gives same result) | Second call on already normalized URL returns same URL |

## Expected Final State

- URL normalization function correctly handles all edge cases
- Function removes trailing slashes while preserving valid URL structure
- Query parameters, ports, and paths are preserved correctly
- Function handles invalid inputs gracefully

## Pass/Fail Criteria

**Pass:**
- Function correctly removes single trailing slash
- Function correctly removes multiple trailing slashes
- Function leaves URLs without trailing slashes unchanged
- Function handles empty string without crashing
- Function handles null/None values without crashing
- Query parameters are preserved
- Trailing slash before query string is removed correctly
- Function is idempotent (normalized URL stays normalized)

**Fail:**
- Function fails to remove trailing slashes
- Function removes characters other than trailing slashes
- Function corrupts query parameters
- Function crashes on empty or null input
- Function modifies already normalized URLs incorrectly
