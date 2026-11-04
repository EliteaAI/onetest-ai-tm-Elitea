---
id: ELITEA-4409
title: "Navigate from Catalog skill Run History to Analytics page"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, catalog, navigation]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to Catalog
- User has executed at least one Catalog skill (e.g., "code-reviewer")
- Catalog skill has run history

## Test Data

| Field | Value |
|-------|-------|
| Base URL | `{{base_url}}` |
| Catalog Skill Example | code-reviewer |
| Expected Skills Count | 50 skills in Catalog |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog from left sidebar | Catalog page opens |
| 2 | Click on "Skills" tab | Skills tab selected, showing skill count (e.g., "Skills (50)") |
| 3 | Select any catalog skill card (e.g., "code-reviewer") | Skill details modal/panel opens |
| 4 | Click three-dot menu (⋮) in skill card or modal | Dropdown menu appears with options: Export, Fork, Share, Run History |
| 5 | Click "Run History" option | Run History modal/page displays with list of runs |
| 6 | In Run History, locate any completed run | Run entry is visible in table |
| 7 | Click three-dot menu (⋮) on the run row | Context menu opens |
| 8 | Click "Analytics" option | System navigates to analytics page |
| 9 | Observe breadcrumbs navigation | Breadcrumbs display path |
| 10 | Verify analytics data loads correctly | Run-specific analytics displayed |

## Expected Final State

Analytics page opens for catalog skill run with:
- Breadcrumbs showing: `Catalog / code-reviewer / Run History / Analytics` OR `Skills / code-reviewer / Run History / Analytics`
- Run data loads correctly
- No navigation errors

## Pass/Fail Criteria

**Pass:**
- Catalog skill Run History is accessible
- Analytics menu option available
- Navigation to analytics page succeeds
- Breadcrumbs display correctly
- Analytics data loads for catalog skill run
- No errors

**Fail:**
- Run History not accessible from catalog skill
- Analytics option missing
- Navigation fails
- Breadcrumbs incorrect or broken
- Data fails to load
- Errors present
