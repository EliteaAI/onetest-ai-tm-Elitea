---
id: ELITEA-4130
title: "The 'Pipeline is running...' indicator is restored after a page refresh or navigating away and back while the pipeline runs"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, feat:pipelines, feat:run_history, issue:3548, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#3548"]
---

# ELITEA-4130: The "Pipeline is running..." indicator is restored after a page refresh or navigating away and back while the pipeline runs

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the running state of a pipeline in chat doesn't depend on the browser tab staying open. If the user refreshes the page, or goes to another page and comes back while the pipeline is still running, the **"Pipeline is running..."** indicator (spinner) must be shown again on that conversation. It must disappear once the run finishes, and the output must appear without a manual refresh.

---

## Preconditions

- A user with access to project **P**, logged in.
- A pipeline **PL** in P that runs for at least **60 seconds**, e.g. a Python Sandbox / Code node that waits (`time.sleep(60)`) and then returns text, so there's time for the steps below.
- A chat conversation **C** with PL as a participant.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In C, send a message to PL to start a run. | Under the message, the **"Pipeline is running..."** indicator with a spinner is shown. |
| 2 | While the run is in progress, **refresh** the page (F5). | C reopens and the indicator is shown again under the same message. There is no empty or broken response block, and the message input is in its running state. |
| 3 | Go to another page (e.g. Agents or Pipelines), wait about 10 seconds, then come back to C from the sidebar. | The indicator is still shown for the running pipeline. |
| 4 | Open a different conversation, then switch back to C. | The indicator is still shown. The other conversation doesn't show it. |
| 5 | Wait for the run to finish without refreshing. | The indicator disappears on its own, and PL's output appears in C. |
| 6 | Refresh the page once more. | Only the finished output is shown. No indicator is shown for the completed run. |

---

## Expected Final State

The running indicator always reflects the real state of the run, wherever the user goes while it runs, and it clears when the run ends.

---

## Pass/Fail Criteria

**Pass:**
- After a refresh, navigating away and back, or switching conversations, the indicator is shown while PL runs.
- It disappears when the run ends, and the output appears without a refresh.

**Fail:**
- After a refresh or navigation, the indicator is missing even though the run is still in progress.
- The indicator stays after the run is finished, or after another refresh.
- The output doesn't appear until the page is refreshed manually.
