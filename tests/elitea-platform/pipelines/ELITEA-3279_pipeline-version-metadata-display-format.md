---
id: ELITEA-3279
title: "Pipeline version displays all required metadata in correct format"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with multiple versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with at least 3 versions |
| Expected timestamp format | "MMM DD, YYYY, hh:mm AM/PM" (e.g., "Jan 15, 2026, 02:30 PM") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipeline with multiple versions | Pipeline loads |
| 2 | Open the version selector dropdown | Dropdown displays list of versions |
| 3 | Select the first version entry and verify version name is clearly visible | Version name is displayed prominently |
| 4 | Verify creation timestamp is in format "MMM DD, YYYY, hh:mm AM/PM" | Timestamp matches required format exactly |
| 5 | Verify creator name and/or email is displayed | Creator information is visible |
| 6 | Check the second version entry for timestamp format | Timestamp matches format (verify AM/PM, date, time) |
| 7 | Check the third version entry | All metadata fields are present |
| 8 | Verify metadata is displayed consistently across all versions | Layout and format are uniform |
| 9 | Verify metadata text does not overlap or truncate incorrectly | All text is readable and properly positioned |
| 10 | Verify spacing and alignment of metadata fields | Visual presentation is clean and aligned |

## Expected Final State

Each Pipeline version entry displays: version name, creation timestamp in "MMM DD, YYYY, hh:mm AM/PM" format, and creator information. All metadata is consistently formatted and clearly visible.

## Pass/Fail Criteria

**Pass:**
- Version name is clearly visible for each entry
- Timestamp displays in exact format "MMM DD, YYYY, hh:mm AM/PM"
- Creator name/email is displayed
- Metadata format is consistent across all versions
- No text overlap or truncation issues
- Proper spacing and alignment

**Fail:**
- Version name is missing or unclear
- Timestamp format is incorrect or inconsistent
- Creator information is missing
- Metadata overlaps or is truncated improperly
- Inconsistent formatting across versions
- Poor spacing or alignment
