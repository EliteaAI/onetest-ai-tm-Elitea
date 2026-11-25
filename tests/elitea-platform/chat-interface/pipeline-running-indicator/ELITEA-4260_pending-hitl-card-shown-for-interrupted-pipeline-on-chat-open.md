---
id: ELITEA-4260
title: "The pending HITL card (Approve / Edit / Reject) is shown when a chat with an interrupted pipeline is opened in another tab or re-entered"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, feat:pipelines, feat:hitl, issue:1977, status-pill, p2]
requirements: ["EliteaAI/elitea_issues#1977"]
---

# ELITEA-4260: The pending HITL card (Approve / Edit / Reject) is shown when a chat with an interrupted pipeline is opened in another tab or re-entered

**Module:** chat-interface · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify that when a pipeline is paused on an interrupt (human-in-the-loop) and the user opens the chat in another tab, or comes back to it, it's clear that the pipeline is waiting for their input. The chat must show the pending HITL message with its **Approve**, **Edit** and **Reject** buttons, not an idle chat with conversation starters. After the user answers, the run must continue.

---

## Preconditions

- A user with access to project **P**, logged in.
- A pipeline **PL** in P with a HITL / interrupt node, followed by at least one more node.
- A chat conversation **C** with PL as a participant.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In tab **A**, send a message to PL in C and wait until it pauses on the HITL node. | The HITL message is shown at the bottom of C (e.g. *"Here is the user input: ..."*) with the **Approve**, **Edit** and **Reject** buttons. |
| 2 | Open the URL of C in a new tab **B**. | Tab B shows the same pending HITL message with Approve / Edit / Reject. Conversation starters are not shown, and C does not look idle. |
| 3 | Close tab B. In tab A, go to another page and then come back to C. | The pending HITL message and its buttons are still shown. |
| 4 | Click **Approve** in tab A. | The buttons go away, and the **"Pipeline is running..."** pill is shown while the next nodes run. |
| 5 | Wait for the run to finish, then refresh the page. | PL's final output is shown. No pill and no active Approve / Edit / Reject buttons are shown. |

---

## Expected Final State

The paused-on-interrupt state is visible as soon as C is opened in any tab, and it clears once the user answers.

---

## Pass/Fail Criteria

**Pass:**
- The pending HITL message with Approve / Edit / Reject is shown in every tab and after every re-entry while PL is paused.
- After Approve, the run continues and finishes normally.

**Fail:**
- C looks idle (conversation starters shown, no HITL buttons) while PL is paused on an interrupt.
- The HITL buttons are still active after the answer is sent, or the run doesn't continue.
