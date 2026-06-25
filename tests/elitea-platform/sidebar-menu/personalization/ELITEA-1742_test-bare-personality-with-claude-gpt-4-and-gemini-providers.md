---
id: ELITEA-1742
title: "Test Bare personality with Claude, GPT-4, and Gemini providers"
priority: critical
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, providers, multi-provider]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1742: Test Bare personality with Claude, GPT-4, and Gemini providers

**Module:** Chat · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Bare personality works consistently with Claude, GPT-4, and Gemini providers

## Preconditions

- User is logged into EliteA platform
- User has access to Claude, GPT-4, and Gemini providers
- User can create new conversations
- Bare personality is available in personality dropdown

## Test Data

- Custom instructions: "Answer in exactly 3 sentences"
- Test prompt: "What is artificial intelligence?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation with Claude provider | New conversation opens with Claude selected |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "Bare" personality | Bare personality selected |
| 4 | Enter custom instructions: "Answer in exactly 3 sentences" | Instructions appear in field |
| 5 | Apply changes and close modal | Changes saved |
| 6 | Send message: "What is artificial intelligence?" | Claude responds with exactly 3 sentences, no personality traits |
| 7 | Create new conversation with GPT-4 provider | New conversation opens with GPT-4 selected |
| 8 | Open Context Management, select Bare with same custom instructions | Settings applied |
| 9 | Send same message: "What is artificial intelligence?" | GPT-4 responds with exactly 3 sentences, no personality traits |
| 10 | Create new conversation with Gemini provider | New conversation opens with Gemini selected |
| 11 | Open Context Management, select Bare with same custom instructions | Settings applied |
| 12 | Send same message: "What is artificial intelligence?" | Gemini responds with exactly 3 sentences, no personality traits |
| 13 | Compare all three responses | All follow custom instructions, none exhibit provider-specific personality variations |

## Expected Final State

- All three providers (Claude, GPT-4, Gemini) respect Bare personality
- Custom instructions applied consistently across all providers
- Responses follow only user-provided instructions, no default personality
- No provider-specific personality leakage or variation

## Pass/Fail Criteria

**Pass:**
- All providers apply Bare personality correctly
- Custom instructions followed by all providers
- No default personality traits appear in any response
- Responses are functionally equivalent across providers
- No errors or provider-specific issues

**Fail:**
- Any provider ignores Bare personality setting
- Custom instructions not applied for any provider
- Provider-specific personality traits appear
- Inconsistent behavior across providers
- Errors or response failures
