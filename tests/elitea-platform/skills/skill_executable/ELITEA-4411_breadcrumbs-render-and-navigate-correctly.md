---
id: ELITEA-4411
title: "Verify breadcrumbs render and navigate correctly"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, navigation, breadcrumbs]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Navigation stack includes: Skills → Skill Detail → Run History → Analytics

## Test Data

| Field | Value |
|-------|-------|
| Expected Breadcrumbs | `Skills / [Skill Name] / Run History / Analytics` |
| For Catalog Skills | May show: `Catalog / [Skill Name] / Run History / Analytics` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill run analytics page | Analytics page displays |
| 2 | Observe breadcrumb trail at top of page | Breadcrumbs visible: `Skills / [skill-name] / Run History / Analytics` |
| 3 | Verify "Skills" or "Catalog" is the first segment | First segment present and clickable |
| 4 | Click first segment ("Skills" or "Catalog") | Navigates to Skills list or Catalog page |
| 5 | Navigate back to analytics page using browser Back button | Returns to analytics page |
| 6 | Click "[Skill Name]" breadcrumb segment | Navigates to skill detail/editor page |
| 7 | Navigate back to analytics page | Returns to analytics page |
| 8 | Click "Run History" breadcrumb segment | Navigates to Run History page |
| 9 | Navigate back to analytics page | Returns to analytics page |
| 10 | Verify "Analytics" segment is not clickable (current page) | "Analytics" appears as plain text, not a link |
| 11 | Verify all navigation works without errors | No console errors, no broken links |

## Expected Final State

Breadcrumbs:
- Display full navigation path
- All segments except "Analytics" are clickable links
- Each link navigates to correct page
- "Analytics" is current page, not clickable
- Navigation works bidirectionally (forward and back)

## Pass/Fail Criteria

**Pass:**
- Breadcrumbs display: `Skills / [name] / Run History / Analytics` (or Catalog variant)
- All segments clickable except "Analytics"
- Each link navigates correctly
- Browser Back/Forward work correctly
- No navigation errors

**Fail:**
- Breadcrumbs missing or incorrectly formatted
- Links don't work or navigate to wrong pages
- "Analytics" is clickable (should not be)
- Navigation errors or broken links
- Browser navigation broken
