---
id: ELITEA-3793
title: "Verify Custom Instructions Only with Bare Mode"
priority: critical
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p0, bare-personality, custom-instructions, system-prompt, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-3793: Verify Custom Instructions Only with Bare Mode

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when "Bare" personality is selected with custom instructions provided, ONLY those custom instructions are sent to the LLM with no EliteA wrapper or branding added.

**Coverage:**
- System prompt contains ONLY custom instructions
- NO additional EliteA branding or wrapper text
- NO DEFAULT_ASSISTANT template prepended or appended
- LLM follows custom instructions correctly
- Instructions are applied immediately

## Preconditions

- User has "Bare" personality selected
- User has prepared custom instructions text
- New conversation can be started
- Network inspector or SDK logging is available

## Test Data

- Personality: Bare
- Custom Instructions: "You are a helpful assistant. Always respond in Spanish."
- Test message: "What is the capital of France?"
- Expected response language: Spanish

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to User Settings → Personalization. | Personalization page opens. |
| 2 | Set Default Personality to "Bare". | "Bare" is selected. |
| 3 | In "Default User Instructions" field, enter: "You are a helpful assistant. Always respond in Spanish." | Instructions entered in text field. |
| 4 | Save the settings. | Settings saved successfully. |
| 5 | Start a new conversation. | New conversation created. |
| 6 | Open browser Developer Tools → Network tab. | Network inspector active. |
| 7 | Send test message: "What is the capital of France?" | Message sent. |
| 8 | Capture the API request to LLM provider. | Request captured in Network tab. |
| 9 | Examine the `system` field content in request payload. | System field is visible. |
| 10 | Verify system field contains ONLY: "You are a helpful assistant. Always respond in Spanish." | Only custom instructions present. |
| 11 | Verify NO additional EliteA branding or wrapper text is added. | No additional text found. |
| 12 | Verify NO DEFAULT_ASSISTANT template is prepended or appended. | No template content found. |
| 13 | Read the LLM response. | Response is received. |
| 14 | Verify the LLM responds in Spanish language. | Response is in Spanish (e.g., "La capital de Francia es París"). |
| 15 | Check SDK logs for bare persona confirmation. | SDK logs confirm bare mode active. |

## Expected Final State

Custom instructions are saved and applied. LLM responds in Spanish, following the custom instruction with no EliteA modifications.

## Pass/Fail Criteria

**Pass:**
- System field contains ONLY the custom instructions
- NO EliteA branding or wrapper added
- NO DEFAULT_ASSISTANT template content
- LLM responds in Spanish (follows custom instruction)
- SDK logs confirm bare persona mode

**Fail:**
- Additional text added beyond custom instructions
- EliteA branding found in system prompt
- DEFAULT_ASSISTANT template present
- LLM does not follow custom instructions (responds in English)
- API errors or system prompt corruption
