---
id: ELITEA-4261
title: "Another project member who opens a shared chat during a pipeline run sees the same status pill"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, feat:pipelines, issue:1977, status-pill, multi-user, p2]
requirements: ["EliteaAI/elitea_issues#1977"]
---

# ELITEA-4261: Another project member who opens a shared chat during a pipeline run sees the same status pill

**Module:** chat-interface · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify that a second user who opens the same conversation while a pipeline is running, or paused on an interrupt, sees the same status pill as the user who started the run, and that the pill clears for them when the run ends.

---

## Preconditions

- Two users, **U1** and **U2**, who are both members of project **P**. Log them in to separate browser sessions (e.g. a normal window and an incognito window).
- A pipeline **PL** in P with a long-running node (at least 60 seconds), then a HITL / interrupt node.
- A chat conversation **C** created by U1 with PL as a participant, which U2 can open (shared conversation or a shared link).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, send a message to PL in C. | U1 sees the **"Pipeline is running..."** pill. |
| 2 | As U2, open C while the long-running node is still in progress. | U2 sees the **"Pipeline is running..."** pill straight away. C does not look idle. |
| 3 | Wait until PL pauses on the HITL node. | Both U1 and U2 see the pending HITL message with the **Approve**, **Edit** and **Reject** buttons. Neither sees conversation starters. |
| 4 | As U1, click **Approve** and wait for the run to finish. | The pill clears for both users, and both see the final output without a refresh. |

---

## Expected Final State

Every user who opens C sees the same run status, and it clears for everyone when the run ends.

---

## Pass/Fail Criteria

**Pass:**
- U2 sees the right state (running pill or pending HITL buttons) as soon as C is opened.
- The pill clears for U2 when the run ends.

**Fail:**
- U2 sees an idle chat while PL is running or paused.
- U2's pill gets out of sync with U1's, or stays after the run ends.
