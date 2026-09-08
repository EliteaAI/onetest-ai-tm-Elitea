---
id: ELITEA-3289
title: "Version selector dropdown opens and displays all versions in Skills"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Private project context is selected
- At least one Skill exists with multiple versions (base, draft, published)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with base, draft named versions, and published versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills section | Skills list page loads |
| 2 | Open a Skill with multiple versions (base, draft, published) | Skill detail view loads |
| 3 | Locate the version selector component | Version selector displays current version name |
| 4 | Click the version selector dropdown | Dropdown opens without errors |
| 5 | Verify all versions are listed in the dropdown | All versions (base, draft named, published) appear in the list |
| 6 | Check browser console for errors | No JavaScript errors in console |

## Expected Final State

Version selector dropdown opens successfully and displays all existing versions without errors.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens smoothly without delay or errors
- All versions (base, draft, published) are visible in the list
- No console errors or UI glitches
- Version list is complete and accurate

**Fail:**
- Dropdown fails to open
- One or more versions missing from the list
- JavaScript errors in console
- UI freezes or crashes
