---
id: ELITEA-2776
title: "Edit with AI preserves unchanged fields when only specific fields are modified"
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
- An existing Agent with the following configuration is open:
  - Name: "Test Agent"
  - Description: "Test description"
  - Instructions: "You are helpful."
  - Welcome Message: "Hello!"
  - 2 Chat Starters configured
  - 1 Toolkit attached
  - 1 Skill attached

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Only improve the instructions" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent with the preconditioned field values and record them | Baseline values confirmed |
| 2 | Click "Edit with AI" and enter "Only improve the instructions" | Prompt accepted |
| 3 | Generate the draft and complete the wizard, applying the changes | Modal closes without error |
| 4 | Verify the Agent's Name | Remains "Test Agent" (unchanged) |
| 5 | Verify the Agent's Description | Remains "Test description" (unchanged) |
| 6 | Verify the Agent's Welcome Message | Remains "Hello!" (unchanged) |
| 7 | Verify the Agent's Chat Starters | Both original Chat Starters remain unchanged |
| 8 | Verify the Agent's Toolkit and Skill attachments | Both remain attached, unchanged |
| 9 | Verify the Agent's Instructions | Updated to reflect the AI suggestion, differing from "You are helpful." |

## Expected Final State

Only the Instructions field is updated; Name, Description, Welcome Message, Chat Starters, Toolkit, and Skill remain exactly as they were before the Edit with AI session.

## Pass/Fail Criteria

**Pass:**
- Only Instructions changes; all other fields remain byte-for-byte identical to their pre-edit values

**Fail:**
- Any field other than Instructions is modified, or Instructions fails to update
