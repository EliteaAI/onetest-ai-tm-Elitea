---
id: ELITEA-1740
title: "Create chat with Bare personality and verify raw model identity"
priority: critical
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1740: Create chat with Bare personality and verify raw model identity

**Module:** Chat · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that chat with Bare personality returns raw model response without any EliteA branding or personality wrapper

## Preconditions

- User is logged in to `{{base_url}}`
- Default Personality in Settings is set to "Bare"

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Personality | Bare |
| Test Message | Who are you and how can you help me? |
| LLM Provider | Claude (Anthropic) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat page | Chat interface loads |
| 2 | Click "+ Create" button to start new chat | New chat is created |
| 3 | Verify chat inherits "Bare" personality (check Context Management if needed) | Chat uses Bare personality |
| 4 | Type message: "Who are you and how can you help me?" | Message is entered in input field |
| 5 | Send message (Enter or Send button) | Message is sent successfully |
| 6 | Wait for AI response (2-3 seconds) | Response begins streaming |
| 7 | Read the complete AI response | Response is fully received |
| 8 | Verify response contains native model identity (e.g., "I'm Claude", "I'm an AI assistant by Anthropic") | Model identifies itself with native identity |
| 9 | Verify response does NOT contain "EliteA", "EliteA Assistant", "EliteA Hub" | No EliteA branding present |
| 10 | Verify response tone is native model style (not EliteA-modified) | Tone and style are unmodified |

## Expected Final State

Chat with Bare personality returns raw model response without any EliteA branding or personality wrapper.

## Pass/Fail Criteria

**Pass:**
- Model responds with its native identity (Claude, GPT, etc.)
- No EliteA branding in response content
- Response tone is unmodified by EliteA system prompt
- No errors during chat creation or messaging

**Fail:**
- Response contains "EliteA" or related branding
- Model behavior shows EliteA personality injection
- Errors occur during chat or message sending
