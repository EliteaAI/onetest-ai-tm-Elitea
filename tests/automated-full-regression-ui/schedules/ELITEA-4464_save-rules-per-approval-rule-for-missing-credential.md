---
id: ELITEA-4464
title: "Schedules — Missing Credential Is a Notice Under Pause and Ask Me and Blocks Save Under Run Without Asking"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:schedules, feat:credentials, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4464: Schedules — Missing Credential Is a Notice Under Pause and Ask Me and Blocks Save Under Run Without Asking

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of the save rule from #7304: a toolkit with a missing credential is a notice with a hint under **Pause and ask me** and the schedule saves; under **Run without asking** the save is refused. Manual source: ELITEA-4459, ELITEA-4458.

---

## Preconditions

- A team project where "Run without asking" is allowed.
- An agent (created by API) with a GitHub toolkit whose credential title doesn't exist.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent → Schedules → new schedule; set a cron and a prompt; select **Pause and ask me**; Save. | The review shows the notice "A toolkit has no usable credential. The run waits until you add one and approve." and the hint "Sign in or add the credentials before the run; otherwise the run waits for you." |
| 2 | Confirm Save. | Saved; the schedule is listed. |
| 3 | Edit the schedule, switch to **Run without asking**, Save. | Save is refused; the credential finding shows as blocking. |
| 4 | Same via API: PUT the schedule with `approval_rule: "run_without_asking"`. | 409. |
| 5 | Switch back to **Pause and ask me** and Save. | Saved. |
| 6 | Hover the ⓘ next to each rule. | The info text for each rule opens. |

---

## Expected Final State

The schedule exists with Pause and ask me.

## Teardown

Delete the schedule and the agent.
