---
id: ELITEA-4629
title: "ELITEA-4629: Tilde Mention Skill in Chat Without Agent Participant"
priority: critical
type: regression
module: chat/skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:chat, tilde-invocation]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4629: Tilde Mention Skill in Chat Without Agent Participant

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that ~skill syntax works in a standalone chat without an agent participant, allowing users to invoke skills using tilde notation.

**Coverage:**
- ~skill autocomplete functionality in chat
- Skill invocation via tilde mention
- Skill executes and returns response
- Works without agent participant present

## Preconditions

- User is logged into {{base_url}}
- At least one skill is available in the project (e.g., "animal-joke")
- Chat session is open WITHOUT an agent participant
- No skill explicitly added as participant

## Test Data

| Field | Value |
|-------|-------|
| Skill name | animal-joke |
| Test message | ~animal |
| Expected autocomplete | animal-joke appears in autocomplete list |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat session without agent participant | Chat interface loads with empty participants panel |
| 2 | Type "~" in the chat input field | Autocomplete dropdown appears |
| 3 | Continue typing "~animal" | Autocomplete shows matching skills (e.g., "animal-joke") |
| 4 | Select "animal-joke" from autocomplete or complete typing "~animal-joke" | Skill reference appears in message input |
| 5 | Complete the message with instructions, e.g., "~animal-joke tell me a joke" | Full message displayed in input |
| 6 | Send the message | Message sends successfully |
| 7 | Observe skill execution | Skill executes and returns response in chat thread |
| 8 | Verify response comes from skill | Response indicates skill execution (e.g., joke appears) |

## Expected Final State

- ~skill syntax recognized and autocompleted in chat without agent
- Skill executes successfully via tilde mention
- Response appears in chat thread
- Tilde invocation works independently of agent participants

## Pass/Fail Criteria

**Pass:**
- Typing ~ triggers autocomplete with available skills
- Skill can be mentioned and invoked via ~skill syntax
- Skill executes and returns response
- Works in chat without agent participant

**Fail:**
- ~ doesn't trigger autocomplete
- Skill mention doesn't invoke skill execution
- No response received from skill
- Feature only works with agent participant present

## Notes

**Source functional tests:** ELITEA-4271
**Regression rationale:** Critical alternate invocation path for skills; ensures ~skill syntax works independently from agent context.
**Selected checkpoints:** Autocomplete behavior, tilde invocation, skill execution without agent.
