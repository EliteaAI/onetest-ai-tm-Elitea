---
id: ELITEA-4481
title: "Schedules — agent and pipeline editor Schedules section: cards, Active / Paused toggle, overflow menu, Manage Schedules"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:pipelines, issue:7011, issue:7338, issue:7426, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7338", "EliteaAI/elitea_issues#7426"]
---

# ELITEA-4481: Schedules — agent and pipeline editor Schedules section: cards, Active / Paused toggle, overflow menu, Manage Schedules

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify the **Schedules** section at the end of the agent and pipeline editors (Figma layout, #7338): one card per schedule, the whole card opens the schedule, the Active / Paused toggle, the ⋮ menu (Run Now, Run History, Export, Delete), **Manage Schedules** and **+ Schedule**, and that cards fit the panel (#7426).

---

## Preconditions

- **Test data:** import [`qa-sch-agent-basic.agent.md`](../../../test-data/schedules/qa-sch-agent-basic.agent.md), [`qa-sch-pipeline-basic.pipeline.md`](../../../test-data/schedules/qa-sch-pipeline-basic.pipeline.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- An agent **AG** with 2 schedules owned by the tester (one Active, one Paused) and 1 schedule owned by another user.
- A pipeline **PL** with 1 schedule.
- The tester is a project admin (for step 9, also an editor).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open AG's editor and scroll to **Schedules**. | One card per schedule: expression (readable), timezone, name, last run + status, next run, **Active / Paused** toggle. No owner on the card. |
| 2 | Resize the window from wide to narrow (down to 320 px). | Cards size to the panel and don't stretch across it (#7426); text stays readable. |
| 3 | Click a card (not the toggle or the menu). | The schedule's details / edit page opens. |
| 4 | Turn the Active schedule to **Paused**. | Toggle shows Paused; Schedules page shows it paused; no cron run starts at its next time. |
| 5 | Turn it back to **Active**. | Next run is shown again. |
| 6 | ⋮ → **Run Now**. | A run starts (see ELITEA-4482); the card's last run shows Running, then the result. |
| 7 | ⋮ → **Run History**. | Run History opens filtered to this schedule. |
| 8 | ⋮ → **Export**. | A YAML file downloads with this schedule only. |
| 9 | ⋮ → **Delete** → confirm. | The card disappears; the schedule is gone from the Schedules page. |
| 10 | **Manage Schedules**. | Opens the Schedules page (filtered to AG if supported). |
| 11 | **+ Schedule**. | The form opens with Type and entity locked to AG. |
| 12 | The other user's schedule card. | **Record**: whether it is shown to the tester, and which actions it offers (Run Now is owner-only). |
| 13 | Repeat steps 1–3 and 6 in PL's editor. | Same behaviour. |
| 14 | Light and dark theme. | Cards and status colours are readable. |

---

## Expected Final State

AG has one schedule left Active; the deleted schedule is gone.

---

## Pass/Fail Criteria

**Pass:**
- Cards, toggle and menu actions work in both editors.

**Fail:**
- A menu action does nothing or acts on the wrong schedule; cards overflow the panel.
