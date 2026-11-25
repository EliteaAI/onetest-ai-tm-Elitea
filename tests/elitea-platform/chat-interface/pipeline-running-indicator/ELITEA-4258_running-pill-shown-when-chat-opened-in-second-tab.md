---
id: ELITEA-4258
title: "The 'Pipeline is running...' pill is shown when the chat is opened in a second browser tab during a run"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, feat:pipelines, issue:1977, status-pill, p2]
requirements: ["EliteaAI/elitea_issues#1977"]
---

# ELITEA-4258: The "Pipeline is running..." pill is shown when the chat is opened in a second browser tab during a run

**Module:** chat-interface · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify that a user who opens a conversation in a second tab while a pipeline is running sees the **"Pipeline is running..."** status pill right away, without waiting for the next pipeline step event. The pill must clear in both tabs when the run ends.

---

## Preconditions

- A user with access to project **P**, logged in.
- A pipeline **PL** in P with at least 2 nodes, where the first node runs for at least **60 seconds** (e.g. a Code node with `time.sleep(60)`), so no new step event arrives for a while.
- A chat conversation **C** with PL as a participant.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In tab **A**, open C and send a message to PL to start a run. | The **"Pipeline is running..."** pill with the animated icon is shown above the message input. |
| 2 | While the first node is still running, copy the URL of C and open it in a new tab **B** of the same browser. | In tab B, C opens with the same pill shown straight away. Conversation starters are not shown, and the chat does not look idle. |
| 3 | Wait in tab B without sending anything until the first node finishes. | The pill stays shown in tab B for the whole time, and new step output appears in tab B as it arrives. |
| 4 | Wait for the run to finish. | The pill disappears in both tabs, and the final output of PL is shown in both tabs without a refresh. |
| 5 | Refresh tab B. | Only the finished output is shown. No pill is shown. |

---

## Expected Final State

Both tabs show the same, correct run state of C at all times, and the pill clears in both when the run ends.

---

## Pass/Fail Criteria

**Pass:**
- Tab B shows the pill as soon as C opens, before any new step event.
- The pill clears in both tabs when the run ends.

**Fail:**
- Tab B shows conversation starters or an idle chat while PL is running.
- The pill only shows up in tab B after a new step starts.
- The pill stays in either tab after the run is finished.
