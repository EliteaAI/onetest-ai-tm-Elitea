---
id: ELITEA-1210
title: "TC-002: Cloud Checkbox Is Absent From the Jira Toolkit Form"
priority: critical
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1210: TC-002: Cloud Checkbox Is Absent From the Jira Toolkit Form

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Cloud checkbox previously in the Jira toolkit form has been completely removed — it must not appear in the visible section, inside Advanced Settings, or anywhere else on the form.

Coverage:
- Cloud checkbox absent from the visible configuration section
- Cloud checkbox absent from Advanced Settings (expanded)
- No hidden or disabled Cloud checkbox remaining

## Preconditions

- Logged in as User A
- Jira toolkit configuration form open (new toolkit)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Jira toolkit creation form | Form renders with all visible fields |
| 2 | Scan all visible fields for a 'Cloud' checkbox | No 'Cloud' checkbox appears in the visible section |
| 3 | Click 'Advanced Settings' to expand the section | Advanced Settings expands |
| 4 | Scan all advanced fields for a 'Cloud' checkbox | No 'Cloud' checkbox appears in Advanced Settings |
| 5 | Inspect the entire form (scroll top to bottom) | No 'Cloud' checkbox or 'Cloud' label exists anywhere on the form |

## Expected Final State

No 'Cloud' checkbox or 'Cloud' label exists anywhere on the form

## Pass/Fail Criteria

PASS:
- Cloud checkbox is completely absent from the entire form
- The word "Cloud" does not appear as a checkbox label anywhere

FAIL:
- Cloud checkbox appears anywhere on the form (visible section, advanced section, or hidden)
