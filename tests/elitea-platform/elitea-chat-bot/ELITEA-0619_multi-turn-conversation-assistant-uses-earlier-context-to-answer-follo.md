---
id: ELITEA-0619
title: "Multi-turn conversation — assistant uses earlier context to answer follow-up questions"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [conversation-memory, context-retention, story:4775, multi-turn, r-2.0.3]
requirements: [4775, 4776]
---
# ELITEA-0619: Multi-turn conversation — assistant uses earlier context to answer follow-up questions

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that within a single support session, the assistant retains the context of previous messages and uses that context to answer follow-up questions accurately. This is the fundamental multi-turn conversational memory test. Without this, every message is isolated and the assistant is useless for real support scenarios.

## Preconditions

Support Assistant is enabled with a context-aware Agent configured.
Tester has the panel open in a fresh session (no previous messages).

## Test Data

Message 1: "My name is TestUser and I am having trouble with pipelines."
Message 2 (follow-up): "What problem did I just mention?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send message 1: "My name is TestUser and I am having trouble with pipelines." | Message sent; assistant acknowledges or responds to the message |
| 2 | Send message 2: "What problem did I just mention?" | The assistant's response references the pipeline issue from message 1 — it does NOT treat this as a fresh, context-free question |
| 3 | Send a third message: "And what is my name?" | Assistant correctly recalls "TestUser" from message 1 |

## Expected Final State

Assistant correctly recalls "TestUser" from message 1

## Pass/Fail Criteria

PASS: Assistant correctly references earlier context in messages 2 and 3.
FAIL: Assistant gives context-free answers to follow-up questions; treats each message as independent.
