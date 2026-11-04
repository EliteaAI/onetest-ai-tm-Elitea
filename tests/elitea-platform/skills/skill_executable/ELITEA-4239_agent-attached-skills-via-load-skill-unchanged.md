---
id: ELITEA-4239
title: "Regression — Agent-Attached Skills via load_skill Unchanged"
priority: critical
type: regression
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, regression, agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6920]
---
# ELITEA-4239: Regression — Agent-Attached Skills via load_skill Unchanged

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that existing agent-attached skill execution via load_skill continues to work unchanged after Skill Run API implementation.

**Coverage:**
- Agent-attached skills execute normally
- load_skill meta-tool functionality preserved
- Skill registry and progressive disclosure unchanged
- No regression in agent + skill integration

## Preconditions

- Logged in to {{base_url}}
- An agent with attached skills exists
- Agent has `<available_skills>` registry in system prompt
- Agent can invoke load_skill meta-tool

## Test Data

- Agent: Agent with 1+ skills attached
- Attached skill: Skill with known functionality
- User input in agent chat: "Use [skill_name] to help with this task"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open agent chat interface. Start new conversation with agent that has attached skills. | Agent chat opens. Skills listed in agent configuration. |
| 2 | Send message that should trigger skill usage: "Use [skill_name] to [perform task]". | Agent receives message and processes it. |
| 3 | Verify agent invokes load_skill meta-tool for the specified skill. | Agent successfully calls load_skill. Skill instructions loaded into context. |
| 4 | Verify agent uses loaded skill instructions to answer. | Agent response incorporates skill instructions and completes task. |
| 5 | Verify skill chip/indicator appears in UI (if applicable). | Skill usage indicated in UI with skill icon/name chip. |
| 6 | Compare behavior with pre-S1 agent+skill execution (if baseline available). | Behavior identical to previous version. No functional changes. |

## Expected Final State

Behavior identical to previous version with no functional changes.

## Pass/Fail Criteria

**Pass:**
- Agent successfully invokes load_skill
- Skill instructions loaded correctly
- Agent uses skill as before S1 implementation
- No errors or changed behavior
- UI indicators work as expected

**Fail:**
- load_skill fails or throws error
- Skill instructions not loaded
- Agent behavior changed from previous version
- Errors in agent+skill execution
