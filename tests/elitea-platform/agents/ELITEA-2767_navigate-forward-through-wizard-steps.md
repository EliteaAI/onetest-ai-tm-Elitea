---
id: ELITEA-2767
title: "User can navigate forward through wizard steps using Next button"
priority: high
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
| 2 | Generate the draft so all steps are produced | Wizard opens on the General step |
| 3 | Verify "Next" button is visible on the General step | Button present |
| 4 | Click "Next" | Wizard advances to the Instructions step |
| 5 | Click "Next" | Wizard advances to the User Interaction step |
| 6 | Click "Next" | Wizard advances to the Tools & Skills step |
| 7 | Click "Next" | Wizard advances to the Summary step |
| 8 | Verify the "Next" button on the Summary step | "Next" is not shown (Summary is the final step) |

## Expected Final State

The wizard advances sequentially through General → Instructions → User Interaction → Tools & Skills → Summary via the Next button, with no Next control on the final Summary step.

## Pass/Fail Criteria

**Pass:**
- Each Next click advances to the correct subsequent step in order, and no Next button appears on Summary

**Fail:**
- Next skips/repeats a step, navigates to the wrong step, or is still present on the Summary step
