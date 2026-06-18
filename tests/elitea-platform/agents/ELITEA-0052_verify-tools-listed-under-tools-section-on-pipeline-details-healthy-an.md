---
id: ELITEA-0052
title: "Verify tools listed under TOOLS section on Pipeline Details (healthy and warning-state)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0052: Verify tools listed under TOOLS section on Pipeline Details (healthy and warning-state)

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that tools previously added to a Pipeline are still correctly listed under the TOOLS section after the rename, including both healthy and warning-state tools.

**Coverage:**
- Tool listing integrity post-rename on Pipeline Details
- Health indicator state for valid and invalid tools

## Preconditions

- Logged in to {{base_url}}
- A Pipeline exists with at least one healthy tool and one invalid/warning-state tool configured
- Browser: Chrome (latest)

## Test Data

Pipeline with a valid Toolkit and an invalid (misconfigured) Toolkit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline Details page for the configured Pipeline | Pipeline Details page opens |
| 2 | Expand the TOOLS section if collapsed | TOOLS section shows all previously added tools |
| 3 | Verify healthy tool is listed with no warning indicators | Tool name is shown, no warning icon |
| 4 | Verify warning-state tool is listed with a warning/alert icon | Tool name is shown with a warning icon (⚠) |
| 5 | Confirm all tools match what was configured before the rename | No tools are missing or duplicated |

## Expected Final State

No tools are missing or duplicated

## Pass/Fail Criteria

**Pass:** All tools listed correctly; health state indicators render as expected
**Fail:** Tools are missing, duplicated, or health indicators do not render
