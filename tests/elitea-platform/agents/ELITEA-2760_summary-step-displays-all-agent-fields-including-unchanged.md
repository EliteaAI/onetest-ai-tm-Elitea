---
id: ELITEA-2760
title: "Summary step displays all Agent fields including unchanged ones"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent with values populated in all configurable fields (Name, Description, Instructions, Welcome Message, Chat Starters, Tools & Skills) is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Only improve the instructions" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent with values in all configurable fields | Baseline values confirmed |
| 2 | Click "Edit with AI" and enter the prompt "Only improve the instructions" | Prompt accepted |
| 3 | Generate the draft and navigate to the Summary step | Summary step renders |
| 4 | Verify the Name field on the Summary step | Name is shown unchanged, displaying the current value |
| 5 | Verify the Description field on the Summary step | Description is shown unchanged, displaying the current value |
| 6 | Verify the Instructions field on the Summary step | Instructions is shown changed, displaying the AI-suggested value |
| 7 | Verify the Welcome Message field on the Summary step | Welcome Message is shown unchanged, displaying the current value |
| 8 | Verify the Chat Starters field on the Summary step | Chat Starters is shown unchanged, displaying the current values |
| 9 | Verify the Tools & Skills section on the Summary step | Tools & Skills is shown unchanged, displaying current attachments |

## Expected Final State

The Summary step is a complete representation of the Agent's post-apply state, covering every field, whether or not it was targeted by the prompt.

## Pass/Fail Criteria

**Pass:**
- All fields are present on the Summary step; targeted fields show suggested values, untargeted fields show current values

**Fail:**
- Any field is missing from the Summary step, or an untargeted field incorrectly shows a suggested/changed value
