---
id: ELITEA-2721
title: "HTML with external CSS references"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file with external CSS link is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | HTML file containing link rel stylesheet href |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or locate HTML with external CSS link | Test file is ready |
| 2 | Open the file in Preview mode | HTML renders in Canvas |
| 3 | Observe styling application | Styling is applied or gracefully degraded |
| 4 | Check for error messages | No error messages shown to user |
| 5 | Verify HTML structure is still readable | Content is accessible |

## Expected Final State

- External CSS loads if accessible from the Preview iframe
- If CSS is blocked (security), HTML renders with default browser styles
- No error messages displayed to user
- HTML structure is still readable

## Pass/Fail Criteria

**Pass:**
- External CSS loads if accessible
- If blocked, HTML renders with default styles
- No error messages to user
- HTML structure remains readable

**Fail:**
- Page fails to load or shows error
- User sees security or network errors
- HTML structure is broken
