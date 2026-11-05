---
id: ELITEA-4459
title: "Schedules — missing credential at run start: the run waits without a chat, approve is refused until the credential is added, then the run starts again"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:credentials, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4459: Schedules — missing credential at run start: the run waits without a chat, approve is refused until the credential is added, then the run starts again

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify #7304 for a toolkit whose credential is missing when the scheduled run starts: with **Pause and ask me** the run waits (no chat yet), the owner adds the credential and approves, and the run starts again. Approving while the credential is still missing is refused. Other start problems (lost access, broken version) fail at once.

---

## Preconditions

- A team project **P**; the tester owns the schedule.
- An agent **AG** with a GitHub toolkit whose credential **gh-main** the owner can't use (deleted, or a personal credential that doesn't exist for the owner).
- The credential **gh-main** can be re-created during the test.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a **Pause and ask me** schedule for AG. Save. | Review notice: "A toolkit has no usable credential. The run waits until you add one and approve." with the hint and the link "Open agent to sign in or add credentials". Saved. |
| 2 | Test run. | Status **Waiting for approval**; **no chat** is created. Run log "Paused for approval: <reason>. Add the credentials, then approve". |
| 3 | Check the run details and notice. | The toolkit and the credential title (gh-main) are named; no secret. One notice. |
| 4 | Open the run. | 'Authorization is required for toolkit "<name>". Provide the credential, then approve.' |
| 5 | Approve without adding the credential. | Refused: "The credential is still missing. Add it, then approve again." The run keeps waiting. |
| 6 | Re-create gh-main, then Approve. | The run starts again. The run log has **one** "Run started" line (no second). The run ends **Success**. |
| 7 | Delete gh-main, Test run (waits), re-create it, Approve, and delete it again right after the approve, before the run starts. | The run ends **Failed** with the credential reason; it does **not** wait a second time. |
| 8 | Delete gh-main, Test run, then **Reject**. | **Failed** "rejected by the owner". |
| 9 | Restore gh-main. Make the owner lose access to AG (remove from the project or change the version so it doesn't expand). Test run. | **Failed** at once; no wait. |
| 10 | Change the rule to **Run without asking** with gh-main missing. Save. | Save blocked (409). A run that starts with gh-main missing ends **Failed** with the reason, never waits. |
| 11 | **Record:** approve, then restart the backend before the run starts (if possible on the env). | Note whether the run starts and whether the credential check repeats. |

---

## Expected Final State

The approved run with the credential re-added ended Success; the other runs ended Failed with their reasons.

---

## Pass/Fail Criteria

**Pass:**
- The run waits only for a missing credential, only under Pause and ask me, and only once.
- Approve is refused while the credential is missing.

**Fail:**
- The run fails in the pre-run check under Pause and ask me (old behaviour).
- An approved run waits a second time, or starts with the credential still missing.
- A lost access right or a broken version makes the run wait.
