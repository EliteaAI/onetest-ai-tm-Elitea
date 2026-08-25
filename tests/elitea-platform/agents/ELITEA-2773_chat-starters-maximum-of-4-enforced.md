---
id: ELITEA-2773
title: "Chat Starters maximum of 4 is enforced in Edit with AI suggestions"
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
- An existing Agent with exactly 3 Chat Starters configured is open

## Test Data

| Field | Value |
|-------|-------|
| Current Chat Starters count | 3 |
| Prompt | "Add more conversation starters" |
| Maximum allowed | 4 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an Agent with 3 Chat Starters configured | Current count confirmed as 3 |
| 2 | Click "Edit with AI" and enter "Add more conversation starters" | Prompt accepted |
| 3 | Generate the draft and navigate to the User Interaction step | Step renders with current and suggested Chat Starters |
| 4 | Count the total number of Chat Starters shown (current + suggested) | Total does not exceed 4 |
| 5 | If the AI suggests additions that would exceed 4, observe the handling | Suggestions are truncated to the maximum, or a message communicates the limit — no way to accept beyond 4 |
| 6 | Complete the wizard and apply changes | Modal closes without error |
| 7 | Verify the final Chat Starters count on the Agent | Count is at most 4 |

## Expected Final State

The Agent's Chat Starters count never exceeds 4 after applying Edit with AI suggestions, regardless of how many were suggested.

## Pass/Fail Criteria

**Pass:**
- The applied Chat Starters count is capped at 4 with clear handling of any excess suggestions

**Fail:**
- The applied count exceeds 4, or excess suggestions are silently dropped without any indication when the limit is reached
