---
id: ELITEA-1746
title: "Verify Context Budget widget tracks tokens correctly with Bare personality"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, context-budget, tokens]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1746: Verify Context Budget widget tracks tokens correctly with Bare personality

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Context Budget widget accurately tracks tokens when using Bare personality

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Context Budget widget is visible and functional
- Bare personality is available in personality dropdown

## Test Data

- Custom instructions: "Be concise and technical"
- Test messages with known approximate token counts

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Note initial Context Budget widget state | Shows 0 or minimal tokens used |
| 3 | Open Context Management modal | Modal opens successfully |
| 4 | Select "Bare" personality | Bare personality selected |
| 5 | Enter custom instructions: "Be concise and technical" | Instructions appear in field |
| 6 | Apply changes and close modal | Changes saved |
| 7 | Check Context Budget widget | Token count includes custom instructions (~5 tokens) |
| 8 | Send message: "What is AI?" (~5 tokens) | Response received |
| 9 | Check Context Budget widget after response | Token count increases by ~5 (input) + response tokens |
| 10 | Send longer message: "Explain machine learning in detail" (~7 tokens) | Response received |
| 11 | Check Context Budget widget | Token count increases proportionally |
| 12 | Switch to different personality (Generic) | Personality changed |
| 13 | Verify token count adjustment | Count reflects removal of Bare custom instructions, addition of Generic system prompt |
| 14 | Switch back to Bare | Bare personality reapplied |
| 15 | Verify token count reflects custom instructions again | Token count includes custom instructions |

## Expected Final State

- Context Budget widget accurately tracks tokens with Bare personality
- Custom instructions tokens are counted
- Token count updates after each message exchange
- Switching personalities updates token count appropriately
- Widget remains accurate throughout conversation

## Pass/Fail Criteria

**Pass:**
- Context Budget widget shows non-zero tokens after applying Bare with custom instructions
- Token count increases after each message
- Token counts are reasonable and proportional to message length
- Switching personalities updates token count correctly
- Widget remains functional and accurate

**Fail:**
- Context Budget widget doesn't count custom instructions
- Token count doesn't increase after messages
- Token counts are wildly inaccurate (off by >20%)
- Widget breaks or shows errors with Bare personality
- Token count not updated when switching personalities
