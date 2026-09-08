---
id: ELITEA-3294
title: "Version metadata displays in correct format in Skills dropdown"
priority: high
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
- Skill with multiple versions exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with versions created at different times by different users |
| Expected timestamp format | "MMM DD, YYYY, hh:mm AM/PM" (e.g., "Jan 15, 2026, 02:30 PM") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with multiple versions | Skill detail view loads |
| 2 | Open the version selector dropdown | Dropdown displays version list |
| 3 | Select a version entry and verify it displays version name | Version name clearly visible |
| 4 | Verify creation timestamp is displayed | Timestamp visible |
| 5 | Verify timestamp format is "MMM DD, YYYY, hh:mm AM/PM" | Format matches specification (e.g., "Jan 15, 2026, 02:30 PM") |
| 6 | Verify creator name and/or email is displayed | Creator info visible |
| 7 | Check multiple versions for consistent formatting | All versions use same format |
| 8 | Verify timestamp shows correct AM/PM designation | AM/PM displayed correctly |
| 9 | Verify metadata doesn't overlap or cause text truncation | Layout is clean, no overlap |
| 10 | Verify all three pieces of information (name, timestamp, creator) are present for each version | All metadata complete |

## Expected Final State

Each version entry displays: version name, creation timestamp in correct format ("MMM DD, YYYY, hh:mm AM/PM"), and creator information, all formatted consistently without layout issues.

## Pass/Fail Criteria

**Pass:**
- Version name clearly visible
- Timestamp in format "MMM DD, YYYY, hh:mm AM/PM"
- Creator name/email displayed
- Consistent formatting across all versions
- No text overlap or truncation issues
- AM/PM designation correct

**Fail:**
- Timestamp in wrong format
- Missing creator information
- Inconsistent formatting between versions
- Text overlap or truncation
- AM/PM missing or incorrect
