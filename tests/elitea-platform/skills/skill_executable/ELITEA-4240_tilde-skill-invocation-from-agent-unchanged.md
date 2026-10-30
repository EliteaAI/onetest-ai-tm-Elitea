---
id: ELITEA-4240
title: "Regression — ~skill Invocation from Agent Chat Unchanged"
priority: critical
type: regression
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, regression, agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4240: Regression — ~skill Invocation from Agent Chat Unchanged

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that explicit ~skill invocation in agent chat continues to work unchanged after Skill Run API implementation.

**Coverage:**
- ~skill syntax recognized in agent chat
- Skill autocomplete functionality preserved
- Explicit skill invocation executes correctly
- No regression in ~skill usage

## Preconditions

- Logged in to {{base_url}}
- An agent with attached skills exists
- Agent chat interface supports ~skill syntax
- Skills have recognizable names

## Test Data

- Agent: Agent with 1+ skills attached
- Attached skill name: e.g., "research_assistant"
- User input: "~research_assistant help me find information about X"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open agent chat interface. Start new conversation with agent that has attached skills. | Agent chat opens. Ready to accept input. |
| 2 | Type "~" in message input field. | Autocomplete dropdown appears showing attached skills. |
| 3 | Select a skill from autocomplete or type full skill name: "~[skill_name]". | Skill name completed in input field. |
| 4 | Complete message: "~[skill_name] help with this task" and send. | Message sent with ~skill invocation. |
| 5 | Verify agent recognizes ~skill invocation and loads skill instructions. | Agent invokes specified skill explicitly. Skill instructions used for response. |
| 6 | Verify agent response incorporates skill's instructions and context. | Response demonstrates skill was invoked and used. |
| 7 | Verify skill chip/indicator appears in UI showing explicit invocation. | UI shows skill was explicitly invoked via ~ syntax. |
| 8 | Compare with pre-S1 ~skill behavior (if baseline available). | Behavior identical to previous version. No changes. |

## Expected Final State

Behavior identical to previous version with no changes.

## Pass/Fail Criteria

**Pass:**
- ~skill autocomplete works
- ~skill invocation recognized by agent
- Skill instructions loaded and used
- Response incorporates skill correctly
- UI indicators work as expected
- No behavior changes from previous version

**Fail:**
- ~skill syntax not recognized
- Autocomplete broken or missing skills
- Skill not invoked despite ~ syntax
- Errors in ~skill execution
- Changed behavior from previous version
