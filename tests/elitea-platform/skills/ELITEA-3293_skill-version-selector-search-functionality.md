---
id: ELITEA-3293
title: "Version selector search filters by name and creator in Skills"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, feat:search, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with multiple versions exists, created by different users

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version names | "base", "Production-v1", "staging-v2", "dev-test", "feature/update-v1" |
| Creators | "Alice Smith (alice@example.com)", "Bob Jones (bob@example.com)" |

## Search by Version Name

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill with multiple versions | Skill loads |
| 2 | Open version selector dropdown | Dropdown opens |
| 3 | Locate search input field | Search field visible |
| 4 | Type "prod" (lowercase) | Only "Production-v1" displayed |
| 5 | Clear and type "PROD" (uppercase) | "Production-v1" displayed (case-insensitive) |
| 6 | Clear and type "v" (partial match) | "Production-v1" and "staging-v2" displayed |
| 7 | Clear the search input | All versions reappear in correct sort order |

## Search by Creator

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | Type "alice" in search field | Only versions by "Alice Smith" displayed |
| 9 | Clear and type "alice@example.com" | Only versions by "Alice Smith" displayed |
| 10 | Clear and type "jones" (last name) | Only versions by "Bob Jones" displayed |

## Special Characters

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Search "feature/" (forward slash) | "feature/update-v1" displayed |
| 12 | Verify no JavaScript errors in console | No errors |

## Clear and No Results

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Type a search query that filters list | Filtered results shown |
| 14 | Clear search input (backspace or clear button) | All versions displayed in correct order |
| 15 | Type "nonexistent-xyz-123" | "No versions found" message displays |
| 16 | Clear the search | All versions reappear |

## Expected Final State

Search filters versions by name and creator, handles special characters, clears correctly, and displays appropriate messages for empty results.

## Pass/Fail Criteria

**Pass:**
- Search filters by version name (case-insensitive, partial match)
- Search filters by creator name and email
- Special characters in version names handled correctly
- Clear button restores full list in correct order
- "No versions found" message displays for no matches
- No console errors

**Fail:**
- Search doesn't filter results
- Case sensitivity issues
- Special characters cause errors
- Clear doesn't restore full list
- No empty state message
- Console errors present
