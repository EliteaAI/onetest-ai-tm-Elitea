---
id: ELITEA-0046
title: "Verify all 5 quick-add buttons are present and functional on Agent Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117, 7380]
requirements: [EliteaAI/elitea_issues#5117, EliteaAI/elitea_issues#7380]
---
# ELITEA-0046: Verify all 5 quick-add buttons are present and functional on Agent Details

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that all five quick-add buttons (+ Toolkit, + MCP, + Agent, + Pipeline, + Modules) remain visible and functional under the TOOLS section on the Agent Details page.

**Coverage:**
- Button presence after rename
- Each button opens the correct add flow
- + Modules button (added in #7380) opens the Modules dropdown

## Preconditions

- Logged in to {{base_url}}
- At least one Agent exists
- Browser: Chrome (latest)

## Test Data

Any existing Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent Details page | Agent Details page is displayed |
| 2 | Locate the TOOLS section | TOOLS section is visible with 5 buttons in order: + Toolkit, + MCP, + Agent, + Pipeline, + Modules |
| 3 | Click "+ Toolkit" | Toolkit selection/configuration dialog opens |
| 4 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 5 | Click "+ MCP" | MCP selection/configuration dialog opens |
| 6 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 7 | Click "+ Agent" | Agent selection dialog opens |
| 8 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 9 | Click "+ Pipeline" | Pipeline selection dialog opens |
| 10 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 11 | Click "+ Modules" | Modules dropdown opens with a "Search modules..." field and the module list |
| 12 | Press Escape | Dropdown closes; TOOLS section still visible |

## Expected Final State

Dialog / dropdown closes; TOOLS section still visible

## Pass/Fail Criteria

**Pass:** All 5 buttons present; each opens the correct dialog or dropdown without errors
**Fail:** Any button is missing, disabled, or opens an incorrect/broken dialog
