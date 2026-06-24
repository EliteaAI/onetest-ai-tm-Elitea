---
id: ELITEA-0013
title: "Verify automatic summarization works with Bare personality"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, summarization, context-budget]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-0013: Verify automatic summarization works with Bare personality

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that automatic summarization functions correctly when using Bare personality

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Context Budget and summarization features are enabled
- Bare personality is available in personality dropdown
- User can trigger summarization (via context limit or manual trigger)

## Test Data

- Custom instructions: "Use technical terminology"
- Multiple test messages to exceed context budget

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "Bare" personality | Bare personality selected |
| 4 | Enter custom instructions: "Use technical terminology" | Instructions appear in field |
| 5 | Set lower context budget (e.g., 2000 tokens) for testing | Budget limit set |
| 6 | Apply changes and close modal | Changes saved |
| 7 | Send multiple messages to exceed context budget | Messages sent successfully |
| 8 | Continue conversation until summarization triggers | Summarization notification or indicator appears |
| 9 | Verify summarization occurred | Context Budget shows reduced token count after summarization |
| 10 | Send new message after summarization | Response received using summarized context |
| 11 | Verify response quality | Response maintains conversation coherence using summary |
| 12 | Verify custom instructions still applied | Response follows "Use technical terminology" instruction |
| 13 | Check Context Management modal | Bare personality and custom instructions still selected |

## Expected Final State

- Automatic summarization triggers when context budget exceeded
- Summarization works correctly with Bare personality
- Custom instructions preserved after summarization
- Conversation coherence maintained with summarized context
- Context Budget widget reflects reduced token count
- Bare personality continues to work post-summarization

## Pass/Fail Criteria

**Pass:**
- Summarization triggers automatically when context budget exceeded
- Token count reduces after summarization
- Bare personality and custom instructions preserved
- Post-summarization responses maintain quality and follow custom instructions
- No errors during or after summarization

**Fail:**
- Summarization doesn't trigger or fails
- Custom instructions lost after summarization
- Personality reverts to default after summarization
- Post-summarization responses lose coherence
- Errors or warnings during summarization process
