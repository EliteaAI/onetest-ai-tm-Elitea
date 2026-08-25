---
id: ELITEA-2758
title: "Cancel or dismiss modal does not apply any changes to the Agent"
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
- An existing Agent with known field values across Name, Description, Instructions, Welcome Message, Chat Starters, Toolkits, and Skills is open

## Test Data

| Field | Value |
|-------|-------|
| Prompt | Any general prompt, e.g. "Improve the agent" |
| Dismiss points | Prompt entry step, a mid-wizard step (e.g. General), Summary step, X button |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and record all current field values | Baseline values captured |
| 2 | Click "Edit with AI", enter a prompt, and cancel/close from the prompt entry step | Modal closes; Agent page shows unchanged values |
| 3 | Re-open Edit with AI, generate a draft, navigate to a wizard step (e.g. General), then cancel/dismiss | Modal closes; Agent page shows unchanged values |
| 4 | Re-open Edit with AI, generate a draft, navigate all the way to the Summary step, then cancel/dismiss | Modal closes; Agent page shows unchanged values |
| 5 | Re-open Edit with AI, generate a draft, and close the modal using the X button from any step | Modal closes; Agent page shows unchanged values |
| 6 | After each dismissal in steps 2–5, refresh the Agent page | All original field values persist after refresh — no partial or full application of suggestions occurred |

## Expected Final State

The Agent configuration is identical to its state before any Edit with AI session was initiated, regardless of which step the modal was dismissed from.

## Pass/Fail Criteria

**Pass:**
- No field is modified after canceling/dismissing from any of the four tested exit points

**Fail:**
- Any field changes (fully or partially) after a cancel/dismiss action from any step
