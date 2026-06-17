---
id: ELITEA-1324
title: "Microphone Permission Denied — Error Handling"
priority: critical
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, error-handling, feature:4499, permissions, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1324: Microphone Permission Denied — Error Handling

**Module:** Voice Input · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when microphone access is blocked by the browser, a clear user-readable error toast is displayed and the chat input remains fully functional for typed text.

**Coverage:**
- Error toast shown when microphone permission is denied
- Error message content is user-readable and actionable
- Chat input field remains usable for typed text after permission denial
- Message can be submitted normally after the permission error

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Microphone permission is BLOCKED for the ELITEA domain in browser site settings (set before the test begins)
- Chat page open
- Browser: Chrome or Edge

## Test Data

- Expected error message: "Microphone access denied. Please allow microphone access in your browser settings."
- Typed test message: "This is a typed message after permission denied"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the microphone icon in the chat input field. | A toast error notification appears with a clear user-readable message about the denied microphone permission. No recording is started. |
| 2 | Read the toast error message content. | Message is user-friendly and includes actionable guidance referencing browser settings (not a raw DOMException or technical error string). |
| 3 | Type "This is a typed message after permission denied" manually into the chat input field. | The input field accepts typed text normally. No microphone-related error persists in the UI. |
| 4 | Submit the typed message using the Send button. | The message is sent and processed correctly. An AI response is received. |

## Expected Final State

The message is sent and processed correctly. An AI response is received.

## Pass/Fail Criteria

**Pass:**
- Toast error message is visible with readable and actionable content after permission denial
- Input field remains functional for typed text
- Message can be submitted and processed after the error

**Fail:**
- No error message shown after permission denial
- Error message displays raw technical text (e.g. NotAllowedError, DOMException)
- Input field becomes unresponsive or broken after microphone denial
