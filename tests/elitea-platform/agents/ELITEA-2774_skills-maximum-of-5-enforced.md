---
id: ELITEA-2774
title: "Skills maximum of 5 is enforced in Edit with AI suggestions"
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
- An existing Agent with exactly 4 Skills attached is open

## Test Data

| Field | Value |
|-------|-------|
| Current Skills count | 4 |
| Prompt | "Add relevant skills for this agent" |
| Maximum allowed per agent version | 5 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an Agent with 4 Skills attached | Current count confirmed as 4 |
| 2 | Click "Edit with AI" and enter "Add relevant skills for this agent" | Prompt accepted |
| 3 | Generate the draft and navigate to the Tools & Skills step | Step renders with current and suggested Skills |
| 4 | Count the total number of Skills shown (current + suggested) | Total does not exceed 5 |
| 5 | If the AI suggests additions that would exceed 5, observe the handling | Suggestions are truncated to the maximum, or a message communicates the limit — no way to accept beyond 5 |
| 6 | Complete the wizard and apply changes | Modal closes without error |
| 7 | Verify the final Skills count on the Agent | Count is at most 5 |

## Expected Final State

The Agent's Skills count never exceeds 5 after applying Edit with AI suggestions, regardless of how many were suggested.

## Pass/Fail Criteria

**Pass:**
- The applied Skills count is capped at 5 with clear handling of any excess suggestions

**Fail:**
- The applied count exceeds 5, or excess suggestions are silently dropped without any indication when the limit is reached
