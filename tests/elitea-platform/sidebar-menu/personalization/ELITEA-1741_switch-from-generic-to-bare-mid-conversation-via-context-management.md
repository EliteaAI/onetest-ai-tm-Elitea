---
id: ELITEA-1741
title: "Switch from Generic to Bare mid-conversation via Context Management"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, context-management, conversation]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1741: Switch from Generic to Bare mid-conversation via Context Management

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that users can switch conversation personality from Generic to Bare mid-conversation via Context Management modal

## Preconditions

- User is logged into EliteA platform
- User has an active conversation with Generic personality selected
- Conversation has at least 2 message exchanges
- Context Management modal is accessible

## Test Data

- Conversation with Generic personality active
- Custom instructions: "Be concise and use bullet points"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open existing conversation with Generic personality | Conversation displays with Generic personality responses |
| 2 | Send message: "What is machine learning?" | Response follows Generic personality style |
| 3 | Click Context Management icon in chat header | Context Management modal opens |
| 4 | In "Persona" section, click personality dropdown | Dropdown shows all 7 options: Generic, Bare, QA, Nerdy, Quirky, Cynical, None |
| 5 | Select "Bare" from dropdown | Dropdown displays "Bare" as selected |
| 6 | Enter custom instructions: "Be concise and use bullet points" | Text appears in custom instructions field |
| 7 | Click "Apply" or close modal | Modal closes, changes saved |
| 8 | Send follow-up message: "Explain neural networks" | Response follows Bare personality with custom instructions applied |
| 9 | Verify response style | Response is concise with bullet points, no Generic personality traits |
| 10 | Reopen Context Management modal | Modal shows "Bare" selected with custom instructions preserved |

## Expected Final State

- Conversation personality switched from Generic to Bare
- New messages follow Bare personality behavior with custom instructions
- Previous Generic messages remain unchanged in conversation history
- Context Management modal reflects current Bare personality setting
- Custom instructions are preserved and applied

## Pass/Fail Criteria

**Pass:**
- Personality switches successfully mid-conversation
- New messages follow Bare personality with custom instructions
- Previous messages retain original Generic style
- Settings persist after modal close
- No errors or console warnings

**Fail:**
- Personality doesn't switch or requires page reload
- Custom instructions not applied to new messages
- Previous messages altered retroactively
- Settings not saved or lost after modal close
- Errors or UI inconsistencies
