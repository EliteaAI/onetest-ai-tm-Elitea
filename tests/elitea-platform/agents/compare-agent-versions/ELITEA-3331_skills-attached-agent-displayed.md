---
id: ELITEA-3331
title: "Skills attached to Agent are displayed correctly in Tools & Skills section of comparison modal"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, bug:6576]
requirements: [EliteaAI/elitea_issues#6304, EliteaAI/elitea_issues#6576]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Skills exist in the system that can be attached to Agents
- Agent exists with 2+ versions having different Skills attached

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Scenarios | Agent with: 0 Skills, 1 Skill, 2+ Skills, 5+ Skills |
| Version 1 Skills | Data Analysis Skill, Report Generator Skill |
| Version 2 Skills | Data Analysis Skill, Report Generator Skill, Code Review Skill |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Agent with 2+ Skills attached (e.g., Data Analysis, Report Generator) | Agent created with Skills attached |
| 2 | Create Version 1 (base) with these Skills | Version 1 saved |
| 3 | Create Version 2 with different Skills (add Code Review Skill) | Version 2 created with 3 Skills |
| 4 | Open Compare Versions modal comparing Version 1 and Version 2 | Modal opens successfully |
| 5 | Navigate to Tools & Skills section | Section loads |
| 6 | Verify **Skills** subsection is displayed in both columns | Skills subsection visible |
| 7 | Verify Version 1 Skills list shows: Data Analysis Skill, Report Generator Skill | All 2 Skills listed correctly for Version 1 |
| 8 | Verify Skill names are visible and readable | Skill names displayed clearly |
| 9 | Verify Version 2 Skills list shows: Data Analysis Skill, Report Generator Skill, Code Review Skill | All 3 Skills listed correctly for Version 2 |
| 10 | Verify differences are highlighted: Code Review Skill appears only in Version 2 | Diff highlighting shows Code Review as addition in v2 |
| 11 | Create new Agent with NO Skills attached | Agent created |
| 12 | Open Compare Versions modal for Agent with no Skills | Modal opens |
| 13 | Navigate to Tools & Skills section and verify Skills subsection shows "No Skills attached" or is empty | Empty state displayed correctly |
| 14 | Create Agent with 1 Skill attached | Agent created |
| 15 | Open Compare Versions modal and verify 1 Skill displays correctly | Single Skill listed |
| 16 | Create Agent with 5+ Skills attached | Agent created with 5+ Skills |
| 17 | Open Compare Versions modal and verify all 5+ Skills are listed without truncation | All Skills displayed, scrollable if needed |

## Expected Final State

Skills attached to Agent are displayed correctly in the Tools & Skills section for all scenarios: 0 Skills, 1 Skill, multiple Skills, and 5+ Skills. Skill names are visible and differences are highlighted.

## Pass/Fail Criteria

**Pass:**
- Skills subsection is displayed in Tools & Skills section
- All attached Skills for each version are listed correctly
- Skill names are visible and readable
- Differences in Skills between versions are highlighted
- Works correctly for 0 Skills, 1 Skill, 2+ Skills, and 5+ Skills scenarios

**Fail:**
- Skills subsection is missing
- Attached Skills are not displayed or list is incomplete
- Skill names are not visible
- No diff highlighting for Skill differences
- UI breaks with 5+ Skills
