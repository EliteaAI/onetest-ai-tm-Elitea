---
id: ELITEA-0425
title: "Verify Unique Filenames for Windows Pasted Screenshots [Parametrized]"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3871]
---
# ELITEA-0425: Verify Unique Filenames for Windows Pasted Screenshots [Parametrized]

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that screenshots pasted from the Windows clipboard into any chat context receive unique filenames instead of "image.png", preventing attachment bucket overwrites.

**Coverage:**
- Unique filename assigned on paste in direct chat
- Unique filename assigned on paste in agent chat
- Unique filename assigned in chat with an agent that has Attachments toolkit enabled
- No filename collision between two screenshots pasted in the same conversation
- Downloaded attachment matches the image displayed in chat (no silent overwrite)

## Preconditions

- Logged in to {{base_url}} on **Windows OS**, Chrome or Edge
- A published Agent is available
- A second Agent with the **Attachments toolkit enabled** is available

## Test Data

| # | Scenario | Navigation |
|---|----------|------------|
| 1 | Direct Chat | Sidebar → Projects → project → Chat |
| 2 | Agent Chat | Sidebar → My Libraries → Agents → open Agent → Chat tab |
| 3 | Chat + Agent (Attachments on) | Sidebar → Projects → project → Chat → add agent with Attachments toolkit |

- **Screenshot A:** any distinct screen region (e.g. top-left quadrant)
- **Screenshot B:** a visually different screen region (e.g. bottom-right quadrant)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the scenario's page. For Scenario 3: open project Chat and add the Attachments-enabled agent. | Chat input is visible and ready. For Scenario 3, the agent is attached to the chat session. |
| 2 | Capture Screenshot A via Win+Shift+S (any screen region). | Screenshot A is copied to the clipboard. |
| 3 | Click into the chat input field and paste Screenshot A (Ctrl+V). | Preview thumbnail appears. The filename shown is NOT 'image.png'. Record this as Filename A. |
| 4 | Send the message containing Screenshot A. | Message is sent. Screenshot A attachment is visible in the conversation thread. |
| 5 | Capture Screenshot B via Win+Shift+S (a different screen region from Screenshot A). | Screenshot B is copied to the clipboard. |
| 6 | Paste Screenshot B (Ctrl+V) into the chat input field in the same conversation. | Preview thumbnail appears. The filename shown is NOT 'image.png' and is DIFFERENT from Filename A. Record this as Filename B. |
| 7 | Send the message containing Screenshot B. | Message is sent. Both messages are visible in the thread with distinct attachment filenames. |
| 8 | Click the download/preview link for the Screenshot A attachment (first message). | The downloaded/previewed image matches Screenshot A content — not Screenshot B. |
| 9 | Click the download/preview link for the Screenshot B attachment (second message). | The downloaded/previewed image matches Screenshot B content — not Screenshot A. |
| 10 | Repeat Steps 1–9 for each remaining scenario in the Test Data table. | All 3 scenarios exhibit consistent unique-filename behavior with no overwrites. |

## Expected Final State

All 3 scenarios exhibit consistent unique-filename behavior with no overwrites.

## Pass/Fail Criteria

**Pass:**
- Both screenshots receive unique filenames (never `image.png`) in all 3 scenarios
- No filename collision between the two screenshots in any scenario
- Each download/preview returns the correct corresponding image

**Fail:**
- Any screenshot is saved as `image.png` in any scenario
- Two screenshots in the same conversation share a filename in any scenario
- Downloading Screenshot A returns Screenshot B content (or vice versa) in any scenario
- Any upload error or missing attachment link appears in any scenario
