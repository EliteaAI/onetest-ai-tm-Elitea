---
id: ELITEA-1208
title: "TC-004: Jira Advanced Settings Contains Exactly Verify SSL, Additional Fields, and Flat Custom Headers"
priority: critical
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1208: TC-004: Jira Advanced Settings Contains Exactly Verify SSL, Additional Fields, and Flat Custom Headers

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after expanding the Advanced Settings accordion in the Jira toolkit form, exactly three fields are shown: "Verify SSL" (toggle), "Additional Fields" (text input), and "Custom Headers" as a flat key-value pair input — with NO expand/collapse toggle of its own.

Coverage:
- Advanced Settings reveals exactly: Verify SSL + Additional Fields + Custom Headers
- Custom Headers is flat — no additional toggle or sub-accordion
- No extra / missing fields inside Advanced Settings

## Preconditions

- Logged in as User A
- Jira toolkit creation form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Jira toolkit creation form | Form renders with all visible fields |
| 2 | Click 'Advanced Settings' to expand the section | Section expands |
| 3 | Count the number of fields inside Advanced Settings | Exactly 3 fields visible: Verify SSL, Additional Fields, Custom Headers |
| 4 | Inspect 'Verify SSL' | Rendered as a toggle/switch; toggling it changes state |
| 5 | Inspect 'Additional Fields' | Rendered as a text/textarea input |
| 6 | Inspect 'Custom Headers' | Rendered as a flat key-value pair input with NO expand/collapse toggle of its own |
| 7 | Check whether Custom Headers has any sub-toggle or sub-accordion | No sub-toggle. Custom Headers is always visible as a flat entry when Advanced Settings is expanded |

## Expected Final State

No sub-toggle. Custom Headers is always visible as a flat entry when Advanced Settings is expanded

## Pass/Fail Criteria

PASS:
- Exactly three fields appear: Verify SSL, Additional Fields, Custom Headers
- Custom Headers has no expand/collapse toggle of its own (flat display)
- Verify SSL is a toggle, Additional Fields is a text input

FAIL:
- Fewer or more than 3 fields shown
- Custom Headers has its own expand/collapse toggle (regression)
- Any field is unlabelled or visually misplaced
