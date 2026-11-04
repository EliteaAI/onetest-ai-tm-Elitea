---
id: ELITEA-4422
title: "Verify Tools tab visibility logic based on tool usage"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, tools, conditional-visibility]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User has access to skill runs with varying tool usage
- Test data includes:
  - Skill run WITH tool usage
  - Skill run WITHOUT tool usage (e.g., v1 skill, tool-less run)

## Test Data

| Field | Value |
|-------|-------|
| Scenario A | Skill run with tool usage → Tools tab VISIBLE |
| Scenario B | Skill run without tool usage → Tools tab HIDDEN |

## Steps - Scenario A: Run with Tool Usage

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to analytics page for a run that used tools | Analytics page opens |
| 2 | Observe tab bar: Costs, Tokens, Health | Three tabs visible |
| 3 | Check if "Tools" tab is visible | Tools tab IS visible in tab bar |
| 4 | Click "Tools" tab | Tools tab opens |
| 5 | Verify tool usage data is displayed | Tool Details table with data shown |

## Steps - Scenario B: Run without Tool Usage

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | Navigate to analytics page for a run without tools | Analytics page opens |
| 7 | Observe tab bar: Costs, Tokens, Health | Three tabs visible |
| 8 | Check if "Tools" tab is visible | Tools tab is NOT visible |
| 9 | Verify only three tabs are shown | Only Costs, Tokens, Health displayed |
| 10 | Verify no broken UI or layout issues | Layout clean, no tab spacing issues |

## Expected Final State

Tools tab visibility:
- **WITH tool usage**: Tools tab appears and is clickable
- **WITHOUT tool usage**: Tools tab hidden completely
- No UI breaks or layout issues in either case
- No "No tools used" message needed (tab simply hidden)

## Pass/Fail Criteria

**Pass:**
- Tools tab visible when run has tool usage
- Tools tab displays tool data correctly
- Tools tab hidden when run has no tool usage
- Only Costs, Tokens, Health visible for tool-less runs
- No layout issues in either scenario

**Fail:**
- Tools tab missing when run has tool usage
- Tools tab visible when run has no tool usage
- Tools tab visible but shows "No tools" message (should be hidden)
- UI broken or layout issues
- Tab navigation doesn't work
