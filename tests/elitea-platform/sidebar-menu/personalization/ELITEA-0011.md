---
id: ELITEA-0011
title: Test Bare personality with empty or no custom instructions
priority: critical
type: functional
module: chat
status: approved
execution_type: manual
tags:
  - personality
  - bare-persona
  - edge-case
  - custom-instructions
requirements:
  - "#5394"
---

# Test Bare personality with empty or no custom instructions

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Bare personality is available in personality dropdown

## Test Data

- Custom instructions: (empty/none)
- Test messages:
  - "What is artificial intelligence?"
  - "Explain machine learning"
  - "How does neural network work?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "Bare" personality | Bare personality selected |
| 4 | Leave custom instructions field empty | Field remains empty |
| 5 | Apply changes and close modal | Changes saved |
| 6 | Send message: "What is artificial intelligence?" | Response is neutral, factual, no personality traits |
| 7 | Verify response tone | Response has no distinctive personality characteristics |
| 8 | Send message: "Explain machine learning" | Response is neutral and informative |
| 9 | Send message: "How does neural network work?" | Response is neutral and informative |
| 10 | Compare with Generic personality response (create test conversation) | Bare responses lack Generic's friendly, conversational tone |
| 11 | Verify no fallback to default personality | Responses remain neutral without personality injection |

## Expected Final State

- Bare personality works without custom instructions
- Responses are neutral, factual, without personality traits
- No fallback to Generic or DEFAULT_ASSISTANT personality
- System behaves gracefully with empty custom instructions
- Responses are coherent and informative despite lack of custom guidance

## Pass/Fail Criteria

**Pass:**
- Bare personality works with empty custom instructions
- Responses are neutral and factual
- No personality traits appear (no Generic fallback)
- Responses remain coherent and useful
- No errors or warnings

**Fail:**
- System requires custom instructions for Bare personality
- Responses show Generic or default personality traits
- System falls back to another personality
- Errors or warnings appear
- Responses are incoherent or unhelpful
