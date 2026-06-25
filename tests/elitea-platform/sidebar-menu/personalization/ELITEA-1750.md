---
id: ELITEA-1750
title: "Verify None personality still falls back to DEFAULT_ASSISTANT"
priority: critical
type: regression
module: personalization
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, none-persona, regression, fallback]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1750: Verify None personality still falls back to DEFAULT_ASSISTANT

**Module:** Personalization · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that None personality correctly falls back to DEFAULT_ASSISTANT behavior

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- None personality is available in personality dropdown
- DEFAULT_ASSISTANT behavior is documented or known

## Test Data

- Test prompts:
  - "What is artificial intelligence?"
  - "Explain neural networks"
  - "How does blockchain work?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "None" personality | None personality selected |
| 4 | Apply changes and close modal | Changes saved |
| 5 | Send message: "What is artificial intelligence?" | Response uses DEFAULT_ASSISTANT behavior |
| 6 | Verify response characteristics | Response matches DEFAULT_ASSISTANT system prompt |
| 7 | Send message: "Explain neural networks" | Response maintains DEFAULT_ASSISTANT behavior |
| 8 | Send message: "How does blockchain work?" | Response maintains DEFAULT_ASSISTANT behavior |
| 9 | Compare with pre-Bare-feature baseline | Behavior matches historical None personality |
| 10 | Verify None still acts as fallback | No custom instructions or personality traits added |

## Expected Final State

- None personality still falls back to DEFAULT_ASSISTANT
- DEFAULT_ASSISTANT behavior unchanged
- None personality provides expected baseline behavior
- No regression from Bare feature addition
- Fallback mechanism works correctly

## Pass/Fail Criteria

**Pass:**
- None personality uses DEFAULT_ASSISTANT system prompt
- Behavior matches pre-Bare baseline for None
- Responses are consistent with DEFAULT_ASSISTANT
- No custom personality traits applied
- Fallback mechanism unchanged

**Fail:**
- None personality behavior changed
- Does not fall back to DEFAULT_ASSISTANT
- Unexpected personality traits appear
- Regression from baseline behavior
- Fallback mechanism broken
