---
id: ELITEA-3278
title: "Pipeline version search filters by name and creator correctly"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, feat:search, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with multiple versions created by different users

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with versions: "base", "Production-v1", "staging-v2", "dev-test", "feature/update-v1" |
| Creators | "Alice Smith (alice@example.com)", "Bob Jones (bob@example.com)", "Alice Johnson (alice.j@example.com)" |

## Steps: Search by Version Name

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipeline and open version selector dropdown | Dropdown opens with all versions |
| 2 | Locate the search input field | Search field is visible |
| 3 | Type "prod" (lowercase) in search field | Only "Production-v1" is displayed |
| 4 | Clear and type "PROD" (uppercase) | "Production-v1" is displayed (case-insensitive) |
| 5 | Clear and type "v" (partial match) | "Production-v1", "staging-v2", "feature/update-v1" are displayed |
| 6 | Clear the search field | All versions reappear in correct sort order |

## Steps: Search by Creator

| # | Action | Expected Result |
|---|--------|-----------------|
| 7 | Type "alice" in search field | Versions by "Alice Smith" and "Alice Johnson" display |
| 8 | Clear and type "alice@example.com" | Only versions by "Alice Smith" display |
| 9 | Clear and type "jones" (last name) | Only versions by "Bob Jones" display |
| 10 | Clear and type "@example.com" (domain) | All versions with "@example.com" creators display |

## Steps: Special Characters

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Search "feature/update" (forward slash) | "feature/update-v1" matches correctly |
| 12 | Search with other special characters (-, _, .) | Matches return correct results |
| 13 | Check browser console | No JavaScript errors |

## Steps: Clear and No Results

| # | Action | Expected Result |
|---|--------|-----------------|
| 14 | Type "nonexistent-xyz-123" | "No versions found" message displays |
| 15 | Clear the search | All versions reappear |

## Expected Final State

Search functionality filters Pipeline versions by name and creator accurately, handles special characters, and displays appropriate messages for no results.

## Pass/Fail Criteria

**Pass:**
- Search filters by version name (case-insensitive, partial match)
- Search filters by creator name and email
- Special characters in version names are handled correctly
- Clear search restores full list in correct order
- "No versions found" message displays when appropriate
- No JavaScript errors

**Fail:**
- Search doesn't filter correctly
- Case sensitivity issues
- Special characters cause errors
- Search results are inaccurate
- "No versions found" message doesn't appear
- JavaScript errors occur
