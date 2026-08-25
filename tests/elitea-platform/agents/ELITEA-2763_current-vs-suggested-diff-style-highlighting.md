---
id: ELITEA-2763
title: "Current vs. Suggested values display with diff-style highlighting"
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
- An existing Agent with Instructions set to "You are a helpful assistant." is open

## Test Data

| Field | Value |
|-------|-------|
| Instructions (current) | You are a helpful assistant. |
| Prompt | "Make the instructions more detailed" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent with Instructions "You are a helpful assistant." | Current value confirmed |
| 2 | Click "Edit with AI" and enter "Make the instructions more detailed" | Prompt accepted |
| 3 | Generate the draft and navigate to the Instructions step | Instructions step renders |
| 4 | Verify a read-only "Current" value is shown displaying "You are a helpful assistant." | Current value displayed and not editable |
| 5 | Verify an editable "Suggested" value is shown with the AI-generated improvement | Suggested value displayed and editable |
| 6 | Verify added content in the diff is highlighted distinctly (e.g. green) | Additions visually highlighted |
| 7 | Verify removed content in the diff is highlighted distinctly (e.g. red) | Removals visually highlighted |
| 8 | Repeat verification of Current/Suggested diff highlighting on the General step | Same diff highlighting behavior observed |
| 9 | Repeat verification of Current/Suggested diff highlighting on the User Interaction step | Same diff highlighting behavior observed |

## Expected Final State

Each text-based wizard step consistently shows a read-only Current value and an editable Suggested value, with clear diff-style highlighting of additions and removals.

## Pass/Fail Criteria

**Pass:**
- Current and Suggested values are both shown with distinct, consistent diff highlighting across General, Instructions, and User Interaction steps

**Fail:**
- Current value is missing/editable, Suggested value is missing/read-only, or diff highlighting is absent/inconsistent
