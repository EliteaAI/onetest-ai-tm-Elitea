---
id: ELITEA-2761
title: "All wizard steps are displayed when user submits general request without specifying fields"
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
- An existing Agent with Name, Description, Instructions, Welcome Message, Chat Starters, Toolkit, and Skill configured is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Make this agent better at helping users" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent's configuration page | Page loads |
| 2 | Click "Edit with AI" CTA | Modal opens at prompt entry step |
| 3 | Enter the general prompt "Make this agent better at helping users" | Prompt text entered |
| 4 | Click "Generate Draft" | Generation starts and completes |
| 5 | Observe the wizard step order after generation | Steps are displayed in order: General, Instructions, User Interaction, Tools & Skills, Summary |
| 6 | Verify the General step contains Name and Description | Both fields are present |
| 7 | Verify the User Interaction step contains Welcome Message and Chat Starters | Both fields are present |

## Expected Final State

The wizard presents all five steps (General, Instructions, User Interaction, Tools & Skills, Summary) in the correct order since the prompt did not target specific fields.

## Pass/Fail Criteria

**Pass:**
- All 5 steps appear in the correct order for a general, non-targeted prompt

**Fail:**
- Any step is missing, duplicated, or out of order
