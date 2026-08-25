---
id: ELITEA-2765
title: "Tools & Skills recommendations display as minicards with checkboxes, not text-editable"
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
- An existing Agent with at least one Toolkit and one Skill attached is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Add relevant tools for code review" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an Agent with existing Toolkits and Skills attached | Current attachments confirmed |
| 2 | Click "Edit with AI" and enter "Add relevant tools for code review" | Prompt accepted |
| 3 | Generate the draft and navigate to the Tools & Skills step | Step renders |
| 4 | Verify currently attached tools/skills are displayed | Current attachments listed |
| 5 | Verify AI-recommended additions are displayed as minicard elements | Recommendations rendered as minicards, not plain text fields |
| 6 | Verify each recommendation minicard has a checkbox for accept/exclude | Checkbox present on each minicard |
| 7 | Attempt to click/type directly into a recommendation minicard's label | No inline text editing is possible |
| 8 | Toggle a recommendation checkbox off, then on | Checkbox state visually updates accordingly (deselected/selected) |

## Expected Final State

Tools & Skills recommendations remain rendered as non-editable minicards with functioning accept/exclude checkboxes.

## Pass/Fail Criteria

**Pass:**
- Recommendations render as minicards with checkboxes, no inline text editing is possible, and checkbox toggling visually updates state

**Fail:**
- Recommendations render as plain editable text, lack checkboxes, or checkbox toggling does not update state
