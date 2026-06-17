---
id: ELITEA-0047
title: "Verify all 4 quick-add buttons are present and functional on Pipeline Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0047: Verify all 4 quick-add buttons are present and functional on Pipeline Details

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that all four quick-add buttons remain visible and functional under the TOOLS section on the Pipeline Details page.

**Coverage:**
- Button presence and functionality after rename on Pipeline Details

## Preconditions

- Logged in to {{base_url}}
- At least one Pipeline exists
- Browser: Chrome (latest)

## Test Data

Any existing Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline Details page | Pipeline Details page is displayed |
| 2 | Locate the TOOLS section | TOOLS section is visible with 4 buttons |
| 3 | Click "+ Toolkit" | Toolkit selection/configuration dialog opens |
| 4 | Dismiss the dialog | Dialog closes |
| 5 | Click "+ MCP" | MCP selection/configuration dialog opens |
| 6 | Dismiss the dialog | Dialog closes |
| 7 | Click "+ Agent" | Agent selection dialog opens |
| 8 | Dismiss the dialog | Dialog closes |
| 9 | Click "+ Pipeline" | Pipeline selection dialog opens |
| 10 | Dismiss the dialog | Dialog closes |

## Expected Final State

Dialog closes

## Pass/Fail Criteria

**Pass:** All 4 buttons present; each opens the correct dialog without errors
**Fail:** Any button is missing, disabled, or broken
