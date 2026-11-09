---
id: ELITEA-4457
title: "Schedules — sensitive tool pause: Waiting for approval, approve continues, reject fails, and the pause text counts tools correctly"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:pipelines, issue:7304, issue:7314, r-2.0.8, issue:7432]
requirements: ["EliteaAI/elitea_issues#7304", "EliteaAI/elitea_issues#7314", "EliteaAI/elitea_issues#7432"]
---

# ELITEA-4457: Schedules — sensitive tool pause: Waiting for approval, approve continues, reject fails, and the pause text counts tools correctly

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the owner's flow for a scheduled run that paused before a listed sensitive tool: the status and notice, approve (the run continues from the paused step), reject ("rejected by the owner"), and the text of the waiting card.

**Suspected bug (from the code):** the pause text adds "(+N more)" by counting the sensitive items in the pause. The worker always repeats a single pause in its list (`hitl_interrupts = [hitl_interrupt]`), and the core counts both, so **one** sensitive tool shows "(+1 more)", and two show "(+2 more)".

---

## Preconditions

- Sensitive Action Tools: `{"artifact": ["create_file"], "github": ["create_pull_request"]}`.
- Agent **AG** with an Artifact toolkit **ART** and a GitHub toolkit **GH**; a "Pause and ask me" schedule owned by the tester.
- A pipeline **PL** with a tool node that calls `create_file` through ART, and its own "Pause and ask me" schedule.

---

## Test Data

| Item | Value |
|------|-------|
| Prompt, one tool | "Create a file `sched-<n>.txt` with the text 'hello'" |
| Prompt, two tools in parallel | "At the same time, create the file `a.txt` and open a pull request …" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Test run AG's schedule with the one-tool prompt. | Status **Waiting for approval** in the schedule's run list, the schedule card and Settings → Schedules. One "needs approval" notice. |
| 2 | Open the run in the runs panel. | Card "Action needed: this run is waiting for you" with "Paused for approval: Artifact · create_file" and "Reject ends the run as Failed: rejected by the owner." |
| 3 | Check the pause text count. | **No** "(+N more)" for a single tool. **Suspected:** "(+1 more)". Compare with the run log line (same text) and the chat (one approval card). |
| 4 | **Record:** the card also says "This run will not start until you approve it." | Note whether this fits a run that already started and paused mid-way. |
| 5 | Open the run's chat and **Approve**. | The tool runs (file created). The run continues from the paused step, not from the start, and ends **Success**. |
| 6 | Test run again and **Reject**. | **Failed**, reason "rejected by the owner". The file was not created. |
| 7 | Test run with the two-tool prompt. | Both tools pause together (or one after the other). Text shows "(+1 more)" when two wait together. **Suspected:** "(+2 more)". Approving continues to the next pause / to the end. |
| 8 | Test run PL's schedule. | Pauses at the tool node with the same text; Approve continues the pipeline; Reject ends it as Failed "rejected by the owner". |
| 9 | Notification links (approval needed, run finished). | Each link opens the right run. |
| 10 | Light theme and dark theme. | The "Action needed" card is readable; light theme uses the orange accent and a lighter panel. |

---

## Expected Final State

Approved runs ended Success after the tool ran; rejected runs ended Failed "rejected by the owner".

---

## Pass/Fail Criteria

**Pass:**
- Status, notice, approve and reject behave as above.
- The "(+N more)" count equals the number of **other** sensitive tools waiting.

**Fail:**
- A single sensitive tool shows "(+1 more)" (known bug [#7432](https://github.com/EliteaAI/elitea_issues/issues/7432): elitea_core `pause_schedule_run` counts the repeated interrupt).
- Approve restarts the run from the beginning, or reject lets the tool run.
