---
id: ELITEA-3319
title: "Agent version comparison displays Instructions, User Interaction, and Tools & Skills sections"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions containing:
  - Different Instructions text
  - Different Welcome Messages
  - Different Chat Starters
  - Different Tools/Skills attached

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Agent | Agent with complete configuration across versions |
| Version 1 | base - has Instructions, Welcome Message, 2 Chat Starters, Tool A, Skill A |
| Version 2 | v1.0 - has different Instructions, Welcome Message, 3 Chat Starters, Tool B, Skill B |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Verify **Instructions** section is displayed | Instructions section visible with section header |
| 3 | Verify Instructions shows editable text areas for both versions | Two text areas visible side-by-side, content is editable |
| 4 | Navigate to **User Interaction** section (via tabs/wizard navigation) | User Interaction section loads |
| 5 | Verify Welcome Message fields are displayed and editable for both versions | Welcome Message text areas visible and editable |
| 6 | Verify Chat Starters fields are displayed with editable text | Chat Starters list visible with text fields editable |
| 7 | Navigate to **Tools & Skills** section | Tools & Skills section loads |
| 8 | Verify list of attached Tools is displayed for both versions | Tools list visible (Tool A in v1, Tool B in v2) |
| 9 | Verify list of attached Skills is displayed for both versions | Skills list visible (Skill A in v1, Skill B in v2) |
| 10 | Verify all sections show content from both versions side-by-side | Content displays in parallel columns |
| 11 | Verify wizard navigation between sections works in both directions | Can navigate forward and backward between all 3 sections |

## Expected Final State

All three Agent sections (Instructions, User Interaction, Tools & Skills) are displayed with correct content from both versions, editable fields are functional, and wizard navigation works.

## Pass/Fail Criteria

**Pass:**
- All three sections are accessible and display correctly
- Instructions and User Interaction sections have editable fields
- Tools & Skills section displays read-only dependency lists
- Content from both versions visible side-by-side
- Wizard navigation works correctly

**Fail:**
- Any section is missing or fails to load
- Editable fields are not functional
- Content from only one version is visible
- Cannot navigate between sections
