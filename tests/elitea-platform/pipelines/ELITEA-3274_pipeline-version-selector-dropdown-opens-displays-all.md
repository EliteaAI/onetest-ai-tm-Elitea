---
id: ELITEA-3274
title: "Pipeline version selector dropdown opens and displays all versions"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role with appropriate permissions
- Private project context is selected
- Pipeline exists with multiple versions (base, draft named versions, published versions)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with at least 3 versions (base, draft, published) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section | Pipelines list view displays |
| 2 | Open a Pipeline that has multiple versions | Pipeline editor/canvas loads with current version |
| 3 | Locate the version selector component in the UI | Version selector is visible |
| 4 | Click the version selector dropdown | Dropdown opens without errors |
| 5 | Verify all existing versions are listed | All versions (base, draft, published) appear in the list |
| 6 | Check browser console for JavaScript errors | No errors logged |

## Expected Final State

Version selector dropdown is open and displays complete list of all Pipeline versions without errors.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens successfully on click
- All Pipeline versions are displayed in the list
- No JavaScript errors in console
- UI is responsive and functional

**Fail:**
- Dropdown fails to open
- Some versions are missing from the list
- JavaScript errors occur
- UI is broken or unresponsive
