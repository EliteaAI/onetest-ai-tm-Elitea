---
id: ELITEA-1722
title: "Verify LLM Native Identity in Bare Mode"
priority: critical
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p0, bare-personality, llm-behavior, identity, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1722: Verify LLM Native Identity in Bare Mode

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when using "Bare" personality mode, the LLM responds with its native identity (Claude, ChatGPT, etc.) rather than EliteA branding or custom persona.

**Coverage:**
- LLM uses its native identity (Claude/ChatGPT)
- NO mention of "EliteA" or "Elitea" in responses
- Response tone is LLM's default (not modified)
- Behavior differs from "Generic" personality

## Preconditions

- User has "Bare" personality selected
- No custom instructions that override identity
- Conversation with Claude or ChatGPT is available
- New conversation can be started

## Test Data

- Personality: Bare
- Custom Instructions: (empty)
- Test messages:
  - "Who are you?"
  - "What is your name?"
  - "Introduce yourself"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Default Personality to "Bare". | "Bare" selected in settings. |
| 2 | Ensure "Default User Instructions" is empty. | No custom instructions set. |
| 3 | Save settings. | Settings saved. |
| 4 | Start a new conversation. | New conversation created. |
| 5 | Send message: "Who are you?" | Message sent. |
| 6 | Read the LLM's response carefully. | Response received. |
| 7 | **If using Claude:** Verify response includes "I'm Claude" or "I am Claude, an AI assistant made by Anthropic". | Claude identifies itself natively. |
| 8 | **If using ChatGPT:** Verify response includes "I'm ChatGPT" or "I am ChatGPT, developed by OpenAI". | ChatGPT identifies itself natively. |
| 9 | Verify NO mention of "EliteA" or "Elitea" anywhere in response. | No EliteA branding found. |
| 10 | Send message: "What is your name?" | Message sent. |
| 11 | Verify LLM responds with its native name (Claude/ChatGPT). | Native name confirmed. |
| 12 | Send message: "Introduce yourself" | Message sent. |
| 13 | Verify response uses LLM's native introduction and tone. | Native introduction provided. |
| 14 | **Comparison test:** Change personality to "Generic" and repeat step 5. | Generic personality selected. |
| 15 | Verify "Generic" mode includes EliteA context or modified behavior. | Generic differs from Bare mode. |

## Expected Final State

LLM consistently responds with its native identity across multiple identity-related queries. No EliteA branding present in Bare mode.

## Pass/Fail Criteria

**Pass:**
- Claude responds with "I'm Claude" or Anthropic attribution
- ChatGPT responds with "I'm ChatGPT" or OpenAI attribution
- NO "EliteA" or "Elitea" mentioned in any responses
- LLM uses native identity, not custom persona
- Response tone is the LLM's default
- Behavior clearly differs from "Generic" personality

**Fail:**
- LLM does not identify itself by native name
- EliteA branding appears in responses
- LLM uses EliteA-specific persona or context
- No difference between "Bare" and "Generic" modes
- Identity responses are vague or generic without native attribution
