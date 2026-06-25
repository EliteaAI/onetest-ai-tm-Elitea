---
id: ELITEA-1743
title: "Test Bare personality with custom instruction to respond in Spanish"
priority: critical
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, localization, custom-instructions]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1743: Test Bare personality with custom instruction to respond in Spanish

**Module:** Chat · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Bare personality respects custom instructions to respond in Spanish with formal tone

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Bare personality is available in personality dropdown

## Test Data

- Custom instructions: "Always respond in Spanish. Use formal tone."
- Test messages:
  - "What is machine learning?"
  - "Explain quantum computing"
  - "How does blockchain work?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "Bare" personality | Bare personality selected |
| 4 | Enter custom instructions: "Always respond in Spanish. Use formal tone." | Instructions appear in field |
| 5 | Apply changes and close modal | Changes saved |
| 6 | Send message: "What is machine learning?" | Response is in Spanish, uses formal tone (usted form) |
| 7 | Send message: "Explain quantum computing" | Response is in Spanish, maintains formal tone |
| 8 | Send message: "How does blockchain work?" | Response is in Spanish, maintains formal tone |
| 9 | Verify no English leakage | All responses entirely in Spanish |
| 10 | Verify formal tone consistency | All responses use formal Spanish (usted, not tú) |

## Expected Final State

- All responses are in Spanish as instructed
- Formal tone (usted form) used consistently
- Custom instructions respected throughout conversation
- No English text appears in responses
- Content quality maintained in target language

## Pass/Fail Criteria

**Pass:**
- All responses entirely in Spanish
- Formal tone (usted) used consistently
- Custom instructions followed for all messages
- Content accuracy maintained in Spanish
- No language mixing or fallback to English

**Fail:**
- Any response contains English
- Informal tone (tú) used instead of formal (usted)
- Custom instructions ignored or partially followed
- Language mixing or inconsistent tone
- Errors or malformed Spanish responses
