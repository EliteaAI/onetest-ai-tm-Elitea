---
id: ELITEA-0423
title: "Custom Target Summary Tokens Value Is Applied to New Chat Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:personalization, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3929]
---
# ELITEA-0423: Custom Target Summary Tokens Value Is Applied to New Chat Conversation

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that after setting a custom Target Summary Tokens value in Personalization settings, a newly created Chat conversation inherits that exact value in its Context Management settings — not the system default of 4096.

**Coverage:**
- Custom Target Summary Tokens (200, 500) is propagated to the new conversation's Context Management modal
- Default value (4096) is also correctly passed through when no customization is done
- Both "Enable context management" and "Enable automatic summarization" toggles are ON as required condition

## Preconditions

- User logged in at elitea
- Private project selected
- Personalization settings accessible via User Profile → Personalization (/app/user-settings/profile)
- Both "Enable context management for new conversations" (Default Context Management) and "Enable automatic summarization" (Default Summarization) toggles are ON

## Test Data

| Run | Target Summary Tokens in Personalization | Expected value in new conversation |
|-----|------------------------------------------|-------------------------------------|
| 1   | 200                                      | 200                                 |
| 2   | 500                                      | 500                                 |
| 3   | 4096 (default)                           | 4096                                |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to elitea | Personalization page loads. Three accordion sections visible: Personalization, Default Context Management, Default Summarization. |
| 2 | Expand 'Default Context Management'. Confirm the 'Enable context management for new conversations' switch is ON. | Toggle is checked/ON. |
| 3 | Expand 'Default Summarization'. Confirm the 'Enable automatic summarization' switch is ON. | Toggle is checked/ON. |
| 4 | Set the Target Summary Tokens field to 200 (Run 1). Click the Save button. | Save succeeds. Visual confirmation of save is shown. |
| 5 | Navigate to Chat (/app/chat). Click the Create button to create a new conversation. | A new, empty conversation is created. |
| 6 | Type 'Hello' in the message input and press Send. | Message is sent. The AI responds. The Context Budget widget appears in the bottom-right area of the chat panel. |
| 7 | Click 'Edit context settings' on the Context Budget widget. | The Context Management modal opens. |
| 8 | Expand the 'Summarization' section inside the modal. Locate the Target Summary Tokens field. Read its current value. | Target Summary Tokens field shows 200 — matching the value set in Personalization. |
| 9 | Close the modal. Return to Personalization, change Target Summary Tokens to 500. Click Save. Repeat steps 5–8. | In the new conversation, Target Summary Tokens shows 500. |
| 10 | Return to Personalization, change Target Summary Tokens to 4096. Click Save. Repeat steps 5–8. | In the new conversation, Target Summary Tokens shows 4096. |

## Expected Final State

In the new conversation, Target Summary Tokens shows 4096.

## Pass/Fail Criteria

**Pass:**
- Target Summary Tokens in new conversation Context Management modal matches the value set in Personalization for all three test data runs
- No default 4096 is shown when a different custom value was saved in Personalization

**Fail:**
- Target Summary Tokens shows 4096 (default) in the new conversation despite a custom value being saved in Personalization
- Target Summary Tokens shows any value other than the one saved in Personalization
- The Context Management modal fails to open or displays an error
