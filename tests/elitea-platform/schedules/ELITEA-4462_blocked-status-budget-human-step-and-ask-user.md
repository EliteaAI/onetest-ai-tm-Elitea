---
id: ELITEA-4462
title: "Schedules — a run is Blocked at start only for a used-up budget or a step that waits for a person"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:pipelines, feat:agents, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4462: Schedules — a run is Blocked at start only for a used-up budget or a step that waits for a person

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify when a scheduled run gets the status **Blocked**: at start, before anything runs, when the owner's budget is used up, or when the agent / pipeline has a step that waits for a person (HITL or Printer node, or the agent's `ask_user` tool). Since #7304, a missing credential or sign-in is **not** Blocked any more. Record whether the owner is told about a Blocked run: in the code, Blocked sends no notice.

---

## Preconditions

- A team project **P**; the tester owns the schedules.
- A pipeline **PL-H** with a **HITL** node, a pipeline **PL-P** with a **Printer** node, an agent **AG-Q** with the internal tool **ask_user** on, and a plain agent **AG**.
- A way to use up the owner's budget (low user or project budget in Admin Portal).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a schedule for PL-H (each approval rule in turn). Save. | The review shows the human step as **blocking**: 'Node "<id>" waits for a person'. **Record** whether Save is refused or allowed. |
| 2 | If saved, Test run. | Status **Blocked**. Run log "Risk check: blocked: Node "<id>" waits for a person". |
| 3 | Same for PL-P (Printer node). | **Blocked**, same reason with its node. |
| 4 | Same for AG-Q. | **Blocked** "The agent can ask the user a question". |
| 5 | Use up the owner's budget. Test run AG's schedule. | **Blocked** "the <scope> budget is used up". |
| 6 | For steps 2–5, check notifications. | **Record**: Expected today, no notice for Blocked. Note whether the owner is told anywhere. |
| 7 | Restore the budget. Make AG's credential missing, rule **Pause and ask me**, Test run. | **Waiting for approval** (not Blocked). |
| 8 | Same with **Run without asking**. | **Failed** with the credential reason (not Blocked). |
| 9 | Run History status filter. | Blocked can be filtered; the blocked runs are listed. |

---

## Expected Final State

Blocked appeared only for the human steps and the used-up budget.

---

## Pass/Fail Criteria

**Pass:**
- Blocked is used only for these cases, with the reasons above.

**Fail:**
- A missing credential or sign-in shows Blocked.
- A human-step pipeline runs and hangs instead of being Blocked.

Step 6 (no notice for Blocked) is recorded and raised with the product owner; it does not fail the case.
