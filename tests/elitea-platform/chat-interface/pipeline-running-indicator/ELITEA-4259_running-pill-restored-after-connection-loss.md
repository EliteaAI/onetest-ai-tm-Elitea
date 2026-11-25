---
id: ELITEA-4259
title: "The 'Pipeline is running...' pill is restored after the network connection drops and comes back during a run"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, feat:pipelines, issue:1977, status-pill, connection-loss, p2]
requirements: ["EliteaAI/elitea_issues#1977"]
---

# ELITEA-4259: The "Pipeline is running..." pill is restored after the network connection drops and comes back during a run

**Module:** chat-interface · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify that a short connection loss during a pipeline run doesn't break the status pill. When the connection comes back, the pill must show the real run state: shown while PL is still running, cleared with the output shown if PL finished while the user was offline.

---

## Preconditions

- A user with access to project **P**, logged in.
- A pipeline **PL** in P that runs for at least **90 seconds** (e.g. a Code node with `time.sleep(90)`).
- A chat conversation **C** with PL as a participant.
- Chrome DevTools is open on the **Network** tab (to switch the connection with the throttling dropdown).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In C, send a message to PL to start a run. | The **"Pipeline is running..."** pill is shown. |
| 2 | In DevTools, set throttling to **Offline** and wait about 15 seconds. | The app shows that the connection is lost (or stays as it is). There is no crash, blank page, or false "finished" state. |
| 3 | Set throttling back to **No throttling** while PL is still running. | After the socket reconnects, the pill is shown again for the running pipeline. There are no duplicate pills or duplicate messages. |
| 4 | Wait for the run to finish. | The pill disappears and PL's output appears without a refresh. |
| 5 | Start a new run, go **Offline**, and stay offline until after PL should have finished (about 100 seconds). Then go back online. | After reconnecting, no pill is shown for the run that finished. PL's output is shown (straight away or after the chat reloads its state), not a stuck "running" pill. |

---

## Expected Final State

After the connection comes back, the pill always shows the real backend state of the run: running or finished.

---

## Pass/Fail Criteria

**Pass:**
- The pill comes back after reconnecting while the run is still in progress.
- The pill is not shown after reconnecting if the run finished during the outage.

**Fail:**
- The pill is missing after reconnecting while PL is still running.
- The pill stays shown forever after the run finished during the outage.
- Duplicate pills or duplicate responses appear after reconnecting.
