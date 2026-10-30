---
id: ELITEA-1735
title: "Skill — Invocation (Explicit, Autonomous, Coexistence)"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:autonomous-invocation, feat:backward-compatibility, regression:merged]
requirements: []
---

# ELITEA-1735: Skill — Invocation (Explicit, Autonomous, Coexistence)

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that skills can be invoked via explicit `~skill` syntax and autonomous context-based invocation, both from agents and conversations. Verify that both invocation methods coexist without conflicts (no double-injection) and that skill formatting applies only when invoked. Success is confirmed when all invocation methods work correctly in both agent and conversation contexts.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- Skills, Agents, and Chat sections are available.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill 1 Name | UpperCase |
| Skill 1 Instructions | Output text in UPPER CASE |
| Skill 2 Name | UnderscoreDelimiter |
| Skill 2 Instructions | Output text with `_` as delimiter between words |
| Skill 3 Name | Robot-Joker |
| Skill 3 Instructions | Tell jokes about robots. Always output in UPPER CASE |
| Agent 1 Name | MultiSkill Agent |
| Agent 1 Instructions | You are a helpful assistant |
| Agent 2 Name | Joker |
| Agent 2 Instructions | Entertain the user with jokes |
| Plain message to Agent 1 | Generate a list of fruits |
| Explicit invocation Skill 1 | ~UpperCase generate a list of fruits |
| Explicit invocation Skill 2 | ~UnderscoreDelimiter generate a list of fruits |
| Autonomous invocation prompt | Convert this to uppercase: hello world |
| Plain message to Agent 2 | Tell me a joke |
| Explicit invocation Skill 3 | ~Robot-Joker Tell me a joke |
| Coexistence test prompt | I want to convert text to uppercase. Make it simple. |

---

## Steps

### Part 1: Explicit Invocation from Agent

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Skill "UpperCase" with instructions "Output text in UPPER CASE" | Skill is created successfully |
| 2 | Create Skill "UnderscoreDelimiter" with instructions "Output text with `_` as delimiter between words" | Skill is created successfully |
| 3 | Create Agent "MultiSkill Agent" with instructions "You are a helpful assistant" | Agent is created successfully |
| 4 | Attach both skills "UpperCase" and "UnderscoreDelimiter" to the agent | Both skills are listed as attached to the agent |
| 5 | Open the agent and send plain message: "Generate a list of fruits" | Agent responds with normal formatting (NOT upper case, NOT underscore delimited) |
| 6 | Send message: "~UpperCase generate a list of fruits" | Agent responds with text in UPPER CASE |
| 7 | Send message: "~UnderscoreDelimiter generate a list of fruits" | Agent responds with text using `_` as delimiter (e.g., "apple_banana_cherry") |

### Part 2: Autonomous Context-Based Invocation from Agent

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | With the same agent "MultiSkill Agent" still open, send message: "Convert this to uppercase: hello world" (without using ~UpperCase syntax) | Agent autonomously invokes "UpperCase" skill and responds "HELLO WORLD" |
| 9 | Verify the skill invocation is visible in the thought process or skill indication | Thought process or UI indicator shows "UpperCase" skill was invoked |

### Part 3: Explicit Invocation from Conversation

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Create Skill "Robot-Joker" with instructions "Tell jokes about robots. Always output in UPPER CASE" | Skill is created successfully |
| 11 | Create Agent "Joker" with instructions "Entertain the user with jokes" | Agent is created successfully |
| 12 | Attach skill "Robot-Joker" to Agent "Joker" | Skill is listed as attached to the agent |
| 13 | Open a Chat conversation and add Agent "Joker" as a participant | Agent "Joker" appears as a participant in the conversation |
| 14 | Send plain message: "Tell me a joke" | Agent responds with a joke in normal formatting (NOT in UPPER CASE) |
| 15 | Send message: "~Robot-Joker Tell me a joke" | Agent responds with a robot joke formatted entirely in UPPER CASE |
| 16 | Verify skill formatting (UPPER CASE) is applied only to the skill-invoked message | Plain message was normal case; skill-invoked message is UPPER CASE |

### Part 4: Coexistence of Explicit and Autonomous Invocation (No Double-Injection)

| # | Action | Expected Result |
|---|--------|-----------------|
| 17 | With Agent "MultiSkill Agent" open, send message: "I want to convert text to uppercase. Make it simple." | Agent autonomously invokes "UpperCase" skill due to context match |
| 18 | Verify the response is in UPPER CASE | Response is in UPPER CASE |
| 19 | Verify in thought process or skill indicator that the skill was invoked ONCE (no double-injection) | Skill invocation appears exactly once in thought process |
| 20 | Send message: "~UpperCase make this uppercase too" | Agent invokes skill via explicit syntax |
| 21 | Verify both explicit (~skill) and autonomous invocation methods work without conflicts | Both methods work correctly; no errors or double-formatting |

---

## Expected Final State

- Plain messages to agents use default behavior without skill formatting
- Explicit `~skill` syntax correctly invokes the specified skill in both agent and conversation contexts
- Autonomous context-based invocation works when message content matches skill purpose
- Both invocation methods coexist without conflicts or double-injection
- Skill invocation is visible in thought process or skill indicator UI
- Skill formatting applies ONLY when skill is invoked (explicit or autonomous)

---

## Pass/Fail Criteria

**Pass:**
- Plain messages do not apply skill formatting
- Explicit `~skill` invocation applies correct skill formatting in agent and conversation
- Autonomous invocation triggers when context matches skill purpose
- Both invocation methods work correctly without double-injection or conflicts
- Skill invocation is visible in thought process/UI indicator
- All skill invocations produce expected formatting

**Fail:**
- Plain messages incorrectly apply skill formatting
- Explicit `~skill` syntax does not invoke the skill or applies wrong skill
- Autonomous invocation fails to trigger when context matches
- Double-injection occurs (skill applied twice)
- Skill invocation is not visible in thought process
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-1735, ELITEA-1736, ELITEA-2609

**Regression rationale:** Consolidated from 3 tests covering skill invocation mechanisms: (1) ELITEA-1735 tests explicit and autonomous invocation in agent context, (2) ELITEA-1736 tests explicit invocation in conversation context, and (3) ELITEA-2609 tests coexistence of both methods without double-injection. These tests cover the same invocation functionality across different contexts and can be merged into a comprehensive invocation test.

**Selected checkpoints:**
- Agent plain message → no skill formatting
- Agent ~skill1 → Skill 1 formatting applied
- Agent ~skill2 → Skill 2 formatting applied
- Agent contextual message → autonomous invocation of matching skill
- Conversation plain message → no skill formatting
- Conversation ~skill → skill formatting applied
- Coexistence test → autonomous invocation triggers, no double-injection
