---
id: ELITEA-1319
title: "Network Interruption During Active Recording"
priority: high
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4499, feat:voice, resilience, network, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1319: Network Interruption During Active Recording

**Module:** Voice Input · **Priority:** High · **Type:** Functional

**Objective:** Verify that a network interruption during an active recording session does not crash or permanently freeze the input field, and that the interface remains usable for typed input after reconnection.

**Coverage:**
- Input field remains accessible and not frozen during network disconnection
- Microphone icon behavior after network drop
- Input field accepts typed text after network restoration
- Known limitation: mic icon may remain in active state after reconnect; user must manually restart recording

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Chat page open
- Microphone permission granted
- User is able to disconnect and reconnect the network during the test (disable/enable wifi or ethernet)
- Browser: Chrome or Edge

## Test Data

- Network disconnection duration: ~5 seconds
- Test typed message after reconnect: "Network restored"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the microphone icon to start recording. Speak a short phrase. Observe transcription appearing in the input field. | Recording is active. Transcription appears in the input field. |
| 2 | Disconnect the network (disable wifi or ethernet) while recording is still active. Wait ~5 seconds. | The input field does not freeze or crash. The UI remains rendered and accessible. |
| 3 | Reconnect the network. Observe the microphone icon state and the input field. | The page remains accessible and the input field is not permanently broken. (Note: mic icon may visually remain in active state — this is a known accepted limitation.) |
| 4 | If the mic icon is still shown as active, click it to stop. Type "Network restored" and submit via the Send button. | Typed text is accepted normally. Message is submitted and processed. Chat functions correctly after network restoration. |

## Expected Final State

Typed text is accepted normally. Message is submitted and processed. Chat functions correctly after network restoration.

## Pass/Fail Criteria

**Pass:**
- Input field does not freeze or crash during or after network disconnection
- Chat input accepts typed text after reconnect
- Message is submitted and processed normally after network restoration

**Fail:**
- Input field freezes and becomes completely unresponsive
- Page crashes and requires a reload to recover
- Typed text is not accepted after network reconnect

**Known Limitation (accepted, not a failure):** After network reconnect, the microphone icon may remain in the active/recording visual state even though transcription has stopped. The user must manually stop and restart recording to continue. This behavior is accepted and not treated as a test failure.
