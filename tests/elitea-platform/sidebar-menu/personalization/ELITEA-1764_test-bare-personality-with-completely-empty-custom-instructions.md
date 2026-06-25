---
id: ELITEA-1764
title: "Test Bare personality with completely empty custom instructions"
priority: high
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, edge-case, empty-input]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1764: Test Bare personality with completely empty custom instructions

**Module:** Chat · **Priority:** High · **Type:** Functional

**Objective:** Verify that Bare personality handles completely empty custom instructions correctly

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Bare personality available in dropdown

## Test Data

- Custom instructions: (completely empty - no whitespace)
- Test messages:
  - "Explain Python"
  - "What is Docker?"
  - "Describe APIs"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens |
| 3 | Select "Bare" personality | Bare selected |
| 4 | Verify custom instructions field appears | Field visible |
| 5 | Leave custom instructions completely empty (no text, no whitespace) | Field empty |
| 6 | Apply changes | Changes saved without error |
| 7 | Send message: "Explain Python" | Response received without error |
| 8 | Verify response characteristics | Response is neutral, factual, no personality traits |
| 9 | Send message: "What is Docker?" | Response received |
| 10 | Verify response maintains neutral tone | No distinctive personality |
| 11 | Send message: "Describe APIs" | Response received |
| 12 | Verify all responses are coherent and useful | Responses informative despite empty instructions |
| 13 | Reopen Context Management modal | Modal opens |
| 14 | Verify Bare still selected with empty instructions | Setting preserved |
| 15 | Check for validation errors or warnings | No errors displayed |

## Expected Final State

- Bare personality accepts completely empty custom instructions
- System saves empty state without errors
- Responses are neutral, factual, and coherent
- No personality traits injected as fallback
- Empty custom instructions treated as valid state

## Pass/Fail Criteria

**Pass:**
- Bare personality works with empty custom instructions
- No validation errors for empty field
- Responses are neutral and coherent
- Empty state persists correctly
- No fallback to other personalities
- System gracefully handles empty input

**Fail:**
- Validation error for empty custom instructions
- System requires custom instructions text
- Responses show personality traits (fallback behavior)
- Empty state not saved or persisted
- Errors or warnings appear
- System behavior inconsistent or broken
