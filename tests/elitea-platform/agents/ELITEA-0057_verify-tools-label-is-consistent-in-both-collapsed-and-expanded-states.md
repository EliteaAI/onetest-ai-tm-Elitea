---
id: ELITEA-0057
title: "Verify \"TOOLS\" label is consistent in both collapsed and expanded states"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0057: Verify "TOOLS" label is consistent in both collapsed and expanded states

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "TOOLS" label is consistently displayed and correctly reads "TOOLS" in both the collapsed and expanded states across all applicable pages and modes.

**Coverage:**
- Label consistency across states (collapsed/expanded)
- Cross-page consistency: Agent Details, Pipeline Details, canvas modes

## Preconditions

- Logged in to {{base_url}}
- Access to at least one Agent and one Pipeline
- Browser: Chrome (latest)

## Test Data

Any existing Agent and Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent Details; note the TOOLS label in expanded state | Label reads "TOOLS" |
| 2 | Collapse the TOOLS section on Agent Details | Label still reads "TOOLS" in collapsed state |
| 3 | Open Pipeline Details; note the TOOLS label in expanded state | Label reads "TOOLS" |
| 4 | Collapse the TOOLS section on Pipeline Details | Label still reads "TOOLS" in collapsed state |
| 5 | Open an Agent in canvas mode from Chat; check label in expanded and collapsed states | Label reads "TOOLS" in both states |
| 6 | Open a Pipeline in canvas mode from Chat; check label in expanded and collapsed states | Label reads "TOOLS" in both states |

## Expected Final State

Label reads "TOOLS" in both states

## Pass/Fail Criteria

**Pass:** \"TOOLS\" label is consistently correct across all pages and states
**Fail:** Label is missing, blank, reads \"TOOLKITS\", or differs between expanded/collapsed states
