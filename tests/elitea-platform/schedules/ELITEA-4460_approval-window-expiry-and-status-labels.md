---
id: ELITEA-4460
title: "Schedules — approval window: the Admin Portal setting decides when a waiting run expires as Failed, and the UI texts match it"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:admin-platform, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4460: Schedules — approval window: the Admin Portal setting decides when a waiting run expires as Failed, and the UI texts match it

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify that a run waiting for approval ends as **Failed** "approval expired" after the window set in Admin Portal → Configuration → Runtime → **Schedules Approval Wait Hours**, with an "approval expired" notice that names that window. Check the texts that describe it.

**Suspected mismatches (from the code):**
- The ⓘ next to **Pause and ask me** says "No answer in **24 hours** ends the run as **Expired**". It is a fixed string; the server uses the setting and ends the run as **Failed**.
- The UI has labels "Expired" and "Cancelled" that the server never sets, and two names for the waiting status ("Waiting for approval", "Awaiting approval").

---

## Preconditions

- Admin Portal access (platform admin).
- A "Pause and ask me" schedule whose run pauses (sensitive tool, ELITEA-4457), owned by the tester.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Admin Portal → Configuration → Runtime → **Schedules Approval Wait Hours**. Check the value and description. | Default 24. Description: "Hours a scheduled run waits for the owner to approve a sensitive tool before it fails. Allowed range: 1–720." **Record**: it mentions only sensitive tools, though sign-in and credential waits use it too. |
| 2 | Try 0, -1 and 721. | Refused (range 1–720). |
| 3 | Set **1** and save (no restart needed). | Saved. |
| 4 | Test run the schedule; leave it waiting. | Waiting for approval. |
| 5 | Wait more than 1 hour. | The run ends **Failed**, reason "approval expired". Notice: 'Schedule "<name>" was not approved in 1 hours and the run stopped'. |
| 6 | Test run again; while it waits, set the window to **3**. Wait more than 1 hour. | The run expires after **1** hour (the window it was parked with) and the notice says 1 hours. |
| 7 | On the schedule page (create and edit) and in **Review risks before scheduling**, open the ⓘ next to **Pause and ask me**. | **Expected:** the text matches the setting and the Failed status. **Suspected:** "No answer in 24 hours ends the run as Expired." Report if so. |
| 8 | Open the ⓘ next to **Run without asking**. | "The run uses sensitive tools on its own and never waits. … A missing sign-in or credential blocks saving." |
| 9 | Run History status filter and status labels of the expired run. | No "Expired" or "Cancelled" status appears on a real run. **Record** whether the filter offers them. |
| 10 | Compare the waiting status label in the run list, run details, schedule card, Settings → Schedules and notifications. | One name everywhere. **Record** any "Awaiting approval" next to "Waiting for approval". |
| 11 | Set the window back to 24. | Saved. |

---

## Expected Final State

The window is 24 hours again. Expired runs are Failed "approval expired".

---

## Pass/Fail Criteria

**Pass:**
- Expiry follows the Admin Portal value the run was parked with; status Failed; the notice names the hours.

**Fail:**
- The run expires after 24 hours whatever the setting, or is shown as a separate "Expired" status.
- The info text contradicts the behaviour (file a text bug).
