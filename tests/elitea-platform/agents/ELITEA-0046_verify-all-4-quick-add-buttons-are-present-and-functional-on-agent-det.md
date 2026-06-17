---
id: ELITEA-0046
title: "Verify all 4 quick-add buttons are present and functional on Agent Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0046: Verify all 4 quick-add buttons are present and functional on Agent Details

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that all four quick-add buttons (+ Toolkit, + MCP, + Agent, + Pipeline) remain visible and functional under the TOOLS section on the Agent Details page.

**Coverage:**
- Button presence after rename
- Each button opens the correct add flow

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
| 2 | Locate the TOOLS section | TOOLS section is visible with 4 buttons |
| 3 | Click "+ Toolkit" | Toolkit selection/configuration dialog opens |
| 4 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 5 | Click "+ MCP" | MCP selection/configuration dialog opens |
| 6 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 7 | Click "+ Agent" | Agent selection dialog opens |
| 8 | Dismiss the dialog | Dialog closes; TOOLS section still visible |
| 9 | Click "+ Pipeline" | Pipeline selection dialog opens |
| 10 | Dismiss the dialog | Dialog closes; TOOLS section still visible |

## Expected Final State

Dialog closes; TOOLS section still visible

## Pass/Fail Criteria

**Pass:** All 4 buttons present; each opens the correct dialog without errors
**Fail:** Any button is missing, disabled, or opens an incorrect/broken dialog
