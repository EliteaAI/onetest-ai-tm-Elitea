---
id: ELITEA-1720
title: "Verify Empty System Prompt with Bare Mode (No Custom Instructions)"
priority: critical
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p0, bare-personality, system-prompt, api-validation, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1720: Verify Empty System Prompt with Bare Mode (No Custom Instructions)

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when "Bare" personality is selected with NO custom instructions, the system message sent to the LLM is truly empty with no EliteA branding or template content.

**Coverage:**
- System field in LLM API request is empty/null/omitted
- NO "EliteA" branding text is present
- NO DEFAULT_ASSISTANT template content
- SDK logs confirm bare persona bypass
- LLM responds normally without errors

## Preconditions

- User has "Bare" personality selected in User Settings
- User has NOT entered any custom instructions
- User has started a new conversation
- Developer tools / network inspector is available
- SDK logging is enabled (debug mode)

## Test Data

- Personality: Bare
- Custom Instructions: (empty)
- Test message: "Hello"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Default Personality to "Bare" in User Settings. | "Bare" is selected. |
| 2 | Ensure "Default User Instructions" field is empty. | Custom instructions field is blank. |
| 3 | Save settings. | Settings saved successfully. |
| 4 | Navigate to Chat interface. | Chat interface loads. |
| 5 | Start a new conversation. | New conversation created. |
| 6 | Open browser Developer Tools → Network tab. | Network inspector is active. |
| 7 | Send a simple message: "Hello". | Message is sent. |
| 8 | Find the API request to LLM provider in Network tab. | API request is captured. |
| 9 | Click on the request and view the request payload (Preview/Response tab). | Request payload is visible. |
| 10 | Locate the `system` or `systemMessage` field in the request. | System field is found. |
| 11 | Verify the system field is empty: `"system": ""` OR `"system": null` OR omitted entirely. | System field is empty/null/omitted. |
| 12 | Check for absence of "EliteA", "Elitea", or branding text. | NO EliteA branding found. |
| 13 | Check for absence of DEFAULT_ASSISTANT template phrases. | NO template content found. |
| 14 | Check SDK logs (if available) for: "bare persona: bypassing all Elitea-injected prompt content". | SDK log message confirms bare mode. |
| 15 | Verify LLM responds normally without errors. | LLM response received successfully. |

## Expected Final State

Conversation continues normally with empty system prompt. No errors logged in console or backend.

## Pass/Fail Criteria

**Pass:**
- System field is empty string, null, or omitted from request
- NO EliteA branding text present
- NO DEFAULT_ASSISTANT template content
- SDK logs show bare persona bypass message
- LLM responds without errors
- No whitespace or hidden characters in system prompt

**Fail:**
- System prompt contains any text (branding, template, etc.)
- EliteA branding found in system message
- DEFAULT_ASSISTANT template content present
- API request errors
- Missing bare persona log confirmation
