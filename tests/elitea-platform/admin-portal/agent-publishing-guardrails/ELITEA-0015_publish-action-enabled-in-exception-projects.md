---
id: ELITEA-0015
title: "Publish Action Enabled in Exception Projects"
priority: high
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, exceptions, guardrails, story:4434, r-2.0.2, admin, p1]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0015: Publish Action Enabled in Exception Projects

**Module:** Agent Publishing Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that when "Block Agent Publishing" guardrail is enabled with specific project exceptions selected, the Publish action remains enabled in exception projects but is disabled in non-exception projects.

## Preconditions

Admin access to configure guardrail
At least 3 projects exist: Project A (Team), Project B (Private), Project C (Team)
Each project has at least one agent with a draft version
elitea_core plugin can be reloaded

## Test Data

Exception projects: Project A, Project B
Non-exception project: Project C
Agent in each project with draft version ready to publish

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Enable "Block Agent Publishing" toggle (set to ON) | Toggle ON, dropdown appears |
| 3 | Select Project A and Project B as exception projects from dropdown | Both projects selected and displayed |
| 4 | Do NOT select Project C (leave it out of exceptions) | Project C is not in the selected list |
| 5 | Click "Save" button | Settings saved, "Reload required" indicator appears |
| 6 | Reload the elitea_core plugin | Plugin reloads successfully |
| 7 | Navigate to an agent in Project A (exception project) | Agent details page in Project A opens |
| 8 | Open Version actions menu for the draft version | Actions menu opens |
| 9 | Locate the "Publish" action | "Publish" action is present |
| 10 | Verify "Publish" action is ENABLED (clickable, not greyed out) | "Publish" is active and clickable |
| 11 | Navigate to an agent in Project B (exception project) | Agent details page in Project B opens |
| 12 | Open Version actions menu for the draft version | Actions menu opens |
| 13 | Verify "Publish" action is ENABLED in Project B as well | "Publish" is active and clickable |
| 14 | Navigate to an agent in Project C (NOT an exception project) | Agent details page in Project C opens |
| 15 | Open Version actions menu for the draft version | Actions menu opens |
| 16 | Verify "Publish" action is DISABLED in Project C | "Publish" is greyed out and not clickable |
| 17 | Attempt to click "Publish" in Project C | Click has no effect, action does not trigger |

## Expected Final State

Click has no effect, action does not trigger

## Pass/Fail Criteria

PASS:
- "Publish" action is enabled (clickable) in exception projects (Project A and B)
- "Publish" action is disabled (greyed out) in non-exception project (Project C)
- Visual distinction is clear between enabled and disabled states
- Clicking disabled "Publish" in non-exception project has no effect

FAIL:
- "Publish" is disabled in exception projects
- "Publish" is enabled in non-exception project
- No visual distinction between enabled/disabled states
- "Publish" can be triggered in non-exception project despite guardrail
