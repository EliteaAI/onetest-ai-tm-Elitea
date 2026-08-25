---
id: ELITEA-2772
title: "Wizard step indicator displays current position in the flow"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent with all configurable fields populated is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | General prompt so all wizard steps appear |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and initiate Edit with AI with a general prompt | Prompt accepted |
| 2 | Generate a draft producing all steps | Wizard opens on the General step |
| 3 | Verify a step indicator showing step names or numbers is visible | Indicator visible and shows General as current |
| 4 | Navigate to the Instructions step | Indicator updates to show Instructions as current |
| 5 | Navigate to the User Interaction step | Indicator updates to show User Interaction as current |
| 6 | Navigate to the Tools & Skills step | Indicator updates to show Tools & Skills as current |
| 7 | Navigate to the Summary step | Indicator updates to show Summary as current and marks it as the final step |

## Expected Final State

The step indicator accurately reflects the wizard's current position at every step, ending with Summary marked as final.

## Pass/Fail Criteria

**Pass:**
- The indicator updates correctly at every step and marks Summary as the final step

**Fail:**
- The indicator does not update, shows an incorrect step, or fails to mark Summary as final
