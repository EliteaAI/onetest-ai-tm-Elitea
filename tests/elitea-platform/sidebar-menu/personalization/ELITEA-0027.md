---
id: ELITEA-0027
title: Verify each conversation can have independent persona setting
priority: high
type: functional
module: conversation
status: approved
execution_type: manual
tags:
  - personality
  - conversation
  - independence
  - multi-conversation
requirements:
  - "#5394"
---

# Verify each conversation can have independent persona setting

## Preconditions

- User is logged into EliteA platform
- User can create multiple conversations
- Context Management available for all conversations

## Test Data

- Conversation 1: Generic personality
- Conversation 2: Bare personality with custom instructions "Be concise"
- Conversation 3: Nerdy personality
- Test message: "What is machine learning?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create first conversation | Conversation 1 opens |
| 2 | Set personality to "Generic" via Context Management | Generic selected |
| 3 | Send message: "What is machine learning?" | Response with Generic personality |
| 4 | Create second conversation | Conversation 2 opens |
| 5 | Set personality to "Bare" | Bare selected |
| 6 | Enter custom instructions: "Be concise" | Instructions entered |
| 7 | Send message: "What is machine learning?" | Response with Bare personality, concise |
| 8 | Create third conversation | Conversation 3 opens |
| 9 | Set personality to "Nerdy" | Nerdy selected |
| 10 | Send message: "What is machine learning?" | Response with Nerdy personality |
| 11 | Switch to Conversation 1 | Conversation 1 displays |
| 12 | Open Context Management, verify personality | Still shows "Generic" |
| 13 | Send follow-up message | Response maintains Generic personality |
| 14 | Switch to Conversation 2 | Conversation 2 displays |
| 15 | Open Context Management, verify settings | Still shows "Bare" with custom instructions |
| 16 | Send follow-up message | Response maintains Bare personality with conciseness |
| 17 | Switch to Conversation 3 | Conversation 3 displays |
| 18 | Open Context Management, verify personality | Still shows "Nerdy" |
| 19 | Send follow-up message | Response maintains Nerdy personality |

## Expected Final State

- Each conversation maintains independent personality setting
- Switching between conversations preserves individual settings
- No cross-contamination of personalities between conversations
- Custom instructions remain conversation-specific
- All conversations function correctly with different personalities

## Pass/Fail Criteria

**Pass:**
- Each conversation has independent personality setting
- Settings preserved when switching between conversations
- No personality cross-contamination
- Custom instructions remain conversation-specific
- All conversations function correctly

**Fail:**
- Personality settings shared across conversations
- Settings lost when switching conversations
- Personality cross-contamination occurs
- Custom instructions leak between conversations
- Errors or inconsistent behavior
