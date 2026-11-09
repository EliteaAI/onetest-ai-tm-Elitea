---
id: ELITEA-4486
title: "Schedules — several owners on one entity: each run uses its owner's credentials, edits never change the owner, and an owner who loses access pauses only own schedules"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:credentials, nfr:security, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011"]
---

# ELITEA-4486: Schedules — several owners on one entity: each run uses its owner's credentials, edits never change the owner, and an owner who loses access pauses only own schedules

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the ownership rules of the epic (comment 1 of #7011 and the design pack): several users own their own schedules on the same agent; every run executes **as its owner** with the owner's private credentials; editing, pausing or re-saving never changes the owner; one user's changes don't touch another's schedules. When an owner loses access to the project, their schedules stop: the next cron run **fails** "owner lost access" and the schedule is **paused** with reason `owner_lost_access`; other owners' schedules keep running.

Observed on stage2 (project 59): schedules of users removed from the project were auto-paused with `owner_lost_access` and their last cron runs failed "owner lost access".

---

## Preconditions

- A team project **P**; users **U1** and **U2** (editors) and an admin **ADM**.
- An agent **AG** with a toolkit that uses a **personal** credential (same credential ID in each user's private project, different accounts / data).
- A second test user **U3** that can be removed from P (step 9).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | U1 and U2 each create a schedule on AG (cron every 5 min, a prompt that reads data through the toolkit). | Two schedules, owners U1 and U2. |
| 2 | Let both run. | Each run log: "Account: <owner> (schedule owner)". Each result shows the owner's own data (from their personal credential). |
| 3 | As ADM, edit U1's schedule (description) and Save. | Owner stays **U1**. U1 gets an "edited by admin" notice. |
| 4 | As ADM, pause and resume U1's schedule. | Owner stays U1. |
| 5 | As U2, try to read / edit / delete U1's schedule (UI URL and API). | 404 "Schedule not found". U1's schedule unchanged. |
| 6 | U1 deletes their personal credential. Next run of U1's schedule. | U1's run fails (or waits under "Pause and ask me", see ELITEA-4459) with the credential reason. **U2's schedule keeps running.** |
| 7 | As ADM, **Change owner** of U1's schedule to U2. | Owner = U2; the approval rule resets to **Pause and ask me**; an audit record / notice exists. |
| 8 | Change owner to a user who is not an active project member (API). | 400 "the new owner is not an active project member". |
| 9 | U3 owns a schedule on AG. Remove U3 from P. Wait for U3's next cron time. | U3's run **fails** "owner lost access"; the schedule is **paused** with reason `owner_lost_access`; U3 can't decide anything. U1's and U2's schedules keep running. |
| 10 | Check U3's paused schedule on the Schedules page. | Shown paused with the reason; Next run empty (known #7421: it may keep the old time). |
| 11 | Add U3 back. | **Record**: whether the schedule stays paused until resumed (expected) or resumes by itself. |

---

## Expected Final State

U1's original schedule is owned by U2; U3's schedule is paused with `owner_lost_access`.

---

## Pass/Fail Criteria

**Pass:**
- Every run uses its owner's identity and credentials; only Change owner changes the owner; a lost owner stops only their own schedules.

**Fail:**
- A run uses another user's credentials or the system user; an edit changes the owner; one user's problem stops other users' schedules.
