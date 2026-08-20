---
id: ELITEA-2073
title: "Chat – Create Agent with AI Build – Click Cancel and Verify Creation is Terminated"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_build_with_ai_cancel_then_generate_echo_agent.TestBuildWithAICancelThenGenerateEchoAgent.test_cancel_then_generate_creates_echo_agent_in_canvas"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1615
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2073: Chat – Create Agent with AI Build – Click Cancel and Verify Creation is Terminated

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking Cancel in the "Build with AI" modal dismisses the modal without generating any agent configuration, and that clicking Generate followed by "Create Agent" correctly populates the canvas with the AI-generated configuration.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is on the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| AI build description | generate an echo agent |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats section from the left sidebar | Chats section is displayed |
| 2 | Click the "+ Chat" button or click the + icon in the message input area and select "Create New Agent" | The "Create New Agent" canvas panel opens on the right side |
| 3 | Verify the canvas panel displays sections: GENERAL (Name, Description, Tags), INSTRUCTIONS, WELCOME MESSAGE, CHAT STARTERS, ADVANCED | All sections are visible |
| 4 | Verify the "Build with AI" button is visible in the top right corner of the GENERAL section | Build with AI button is visible |
| 5 | Click the "Build with AI" button | The "Build with AI" modal opens with a text area |
| 6 | Verify the modal displays placeholder text and has "Cancel" and "Generate" buttons | Modal displays correctly; Generate is disabled until text is entered |
| 7 | Type "generate an echo agent" in the text area | Generate button becomes enabled (blue/cyan) |
| 8 | Click the "Cancel" button | The "Build with AI" modal closes immediately |
| 9 | Verify no agent generation takes place and the canvas remains open with empty fields | Canvas remains open; no configuration has been auto-generated |
| 10 | Click the "Build with AI" button again | The modal opens again with empty text area |
| 11 | Type "generate an echo agent" and click the "Generate" button | Modal shows loading indicator "Generating agent draft..." with spinner |
| 12 | Wait for AI generation to complete | Confirmation dialog appears with Name, Description, and Instructions sections plus "Back to prompt" and "Create Agent" buttons |
| 13 | Click the "Create Agent" button | Dialog closes; canvas populates with generated agent configuration |
| 14 | Verify the canvas shows Name "Echo Agent", populated Description and Instructions | Canvas shows generated configuration with detailed instructions |
| 15 | Verify the agent is in "Editing..." state as indicated in the canvas | Editing state is shown |

---

## Expected Final State

The "Build with AI" Cancel button correctly dismisses the modal without triggering generation. The Generate + Create Agent flow populates the canvas with the AI-generated agent configuration.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel dismisses the modal without creating any configuration; Generate and Create Agent flow correctly populates the canvas.

**Fail:**
- Any step produces an error or unexpected result.
- Cancel triggers generation, or Generate/Create Agent flow fails to populate the canvas.
