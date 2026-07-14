---
id: ELITEA-1736
title: "Interact with Skills from Conversation"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: automation/tests/ui/skills/test_skill_conversation_interaction.py::TestInteractWithSkillsFromConversation::test_interact_with_skills_from_conversation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/205
---

# ELITEA-1736: Interact with Skills from Conversation

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that skills attached to an agent participant in a chat conversation can be invoked using the `~skill` syntax, and that the agent's default response does not apply skill formatting unless explicitly triggered.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills, Agents, and Chat sections are available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill name | Robot-Joker |
| Skill instructions | Tell jokes about robots. Always output in UPPER CASE |
| Agent name | Joker |
| Agent instructions | Entertain the user with jokes |
| Plain message | Tell me a joke |
| Skill-invoked message | `~Robot-Joker Tell me a joke` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Skill named "Robot-Joker" with instructions: "Tell jokes about robots. Always output in UPPER CASE" | Skill is created and saved successfully |
| 2 | Create Agent named "Joker" with instructions: "Entertain the user with jokes" and attach the "Robot-Joker" skill | Agent is created with the skill listed as attached |
| 3 | Open a Chat conversation and add Agent "Joker" as a participant | Agent "Joker" appears as a participant in the conversation |
| 4 | Send the plain message: "Tell me a joke" | Agent responds with a joke; response is NOT in UPPER CASE formatting |
| 5 | Send the message: `~Robot-Joker Tell me a joke` | Agent responds with a robot joke formatted entirely in UPPER CASE |

---

## Expected Final State

The agent in the chat conversation responds to plain messages with its default behavior (no UPPER CASE), and responds to skill-invoked messages (`~Robot-Joker`) with the skill's defined UPPER CASE formatting.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Plain message response is a joke without UPPER CASE; skill-invoked response is a robot joke in UPPER CASE.

**Fail:**
- Any step produces an error or unexpected result.
- UPPER CASE formatting is applied to the plain message response, or skill invocation does not trigger UPPER CASE output.
