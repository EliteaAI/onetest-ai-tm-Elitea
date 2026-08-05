---
id: ELITEA-1735
title: "Interact with Skills from Agent"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_skill_agent_interaction.TestInteractWithSkillsFromAgent.test_interact_with_skills_from_agent
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/203
---

# ELITEA-1735: Interact with Skills from Agent

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that skills attached to an agent can be invoked selectively via the `~skill` syntax or autonomously based on context, and that the agent's default response does not apply skill formatting unless explicitly or contextually triggered.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill 1 instructions | Output text in UPPER CASE |
| Skill 2 instructions | Output text with `_` as delimiter |
| Agent setup | Attach both skills to the agent |
| Skill 1 invocation syntax | `~skill1 <prompt>` |
| Skill 2 invocation syntax | `~skill2 <prompt>` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Skill 1 with instructions to output text in UPPER CASE | Skill 1 is created and saved successfully |
| 2 | Create Skill 2 with instructions to output text with `_` as delimiter | Skill 2 is created and saved successfully |
| 3 | Create an Agent and attach both Skill 1 and Skill 2 to it | Agent is created with both skills listed as attached |
| 4 | Send a plain message to the Agent asking it to generate some text | Agent responds with text that is NOT in upper case and does NOT use `_` as delimiter |
| 5 | Send a message invoking Skill 1 using `~skill1 <prompt>` syntax | Agent responds with text formatted in UPPER CASE |
| 6 | Send a message invoking Skill 2 using `~skill2 <prompt>` syntax | Agent responds with text using `_` as delimiter |
| 7 | Send a message that contextually matches Skill 1 without using `~skill1` (e.g., "convert this to uppercase: hello world") | Agent autonomously invokes Skill 1 and responds in UPPER CASE |
| 8 | Verify that explicit `~skill` syntax and autonomous invocation coexist | Both invocation methods work correctly without conflicts |

---

## Expected Final State

The agent correctly differentiates between plain requests and skill-invoked requests: plain messages use the agent's default behavior, while `~skillN` prefixed messages or contextually matching messages apply the corresponding skill's formatting rules. Both explicit (`~skill`) and autonomous invocation methods work correctly and coexist without conflicts.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Plain messages do not apply skill formatting; skill-invoked messages (explicit or autonomous) apply the correct skill's formatting.
- Both explicit `~skill` syntax and autonomous context-based invocation work correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Skill formatting is applied to plain messages, or the `~skill` invocation does not trigger the correct skill behavior.
- Autonomous invocation fails to trigger when context matches.
