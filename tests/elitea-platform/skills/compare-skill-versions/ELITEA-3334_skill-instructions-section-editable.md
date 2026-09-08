---
id: ELITEA-3334
title: "Skill comparison displays Instructions section with editable fields for both versions"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Skill exists with 2+ versions containing different Instructions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version 1 Instructions | "This skill analyzes data and generates reports." |
| Version 2 Instructions | "This skill performs advanced data analysis and generates comprehensive reports with visualizations." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Skill | Modal opens successfully |
| 2 | Verify **Instructions** section is displayed | Instructions section visible with section header |
| 3 | Verify both versions show editable text areas for Instructions | Two text areas visible side-by-side, content is editable |
| 4 | Verify Version 1 content matches the actual instructions: "This skill analyzes data and generates reports." | Correct content displayed for Version 1 |
| 5 | Verify Version 2 content matches the actual instructions: "This skill performs advanced data analysis..." | Correct content displayed for Version 2 |
| 6 | Verify NO other sections are displayed (Skills only have Instructions) | Only Instructions section visible, no User Interaction or Tools & Skills sections |
| 7 | Click on Version 1 Instructions field | Field is editable, cursor appears |
| 8 | Click on Version 2 Instructions field | Field is editable, cursor appears |

## Expected Final State

Skill comparison displays only the Instructions section with editable text areas for both versions showing correct content.

## Pass/Fail Criteria

**Pass:**
- Instructions section is displayed and accessible
- Both versions show editable text areas
- Content matches actual instructions from each version
- No other sections are displayed (Skills have Instructions only)

**Fail:**
- Instructions section is missing
- Text areas are read-only
- Content does not match actual instructions
- Other sections are incorrectly displayed
