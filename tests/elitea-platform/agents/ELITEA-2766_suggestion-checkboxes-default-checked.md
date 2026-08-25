---
id: ELITEA-2766
title: "Suggestion checkboxes default to checked state"
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
| Prompt | General prompt requesting overall improvement |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and initiate Edit with AI with a general prompt | Prompt accepted |
| 2 | Generate the draft | Wizard renders with all steps |
| 3 | Navigate to the General step and inspect the Name/Description suggestion checkboxes | Both checkboxes are checked by default |
| 4 | Navigate to the Instructions step and inspect its suggestion checkbox | Checkbox is checked by default |
| 5 | Navigate to the User Interaction step and inspect Welcome Message/Chat Starters checkboxes | All are checked by default |
| 6 | Navigate to the Tools & Skills step and inspect each recommended tool/skill checkbox | All are checked by default |

## Expected Final State

Every suggestion checkbox across every wizard step defaults to the checked/active state without any manual interaction.

## Pass/Fail Criteria

**Pass:**
- All suggestion checkboxes across General, Instructions, User Interaction, and Tools & Skills default to checked

**Fail:**
- Any suggestion checkbox defaults to unchecked
