---
id: ELITEA-4479
title: "Schedules page — list, columns, filters, search, sort and what each project role sees"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:pipelines, issue:7011, issue:7338, issue:7421, issue:7435, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7338"]
---

# ELITEA-4479: Schedules page — list, columns, filters, search, sort and what each project role sees

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the **Schedules** page (main navigation item after Pipelines, route `/schedules`): the columns, filters, search, sort and paging, and that a project admin sees every schedule of the project while an editor sees only own schedules and a viewer has no access.

Known bugs covered: [#7421](https://github.com/EliteaAI/elitea_issues/issues/7421) (a paused schedule keeps its old Next run and sorts by it) and [#7435](https://github.com/EliteaAI/elitea_issues/issues/7435) (the Running filter drops a schedule after a skipped cron overlap; fix on main, not in 2.0.8).

---

## Preconditions

- A team project **P** with a project admin **ADM**, an editor **ED** and a viewer **VW**.
- In P, at least: 2 agent schedules and 2 pipeline schedules owned by ADM, 1 schedule owned by ED, one of ADM's schedules **paused**, and schedules whose last run is Success, Failed and Awaiting approval.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM, open the main navigation. | A **Schedules** item is shown right after **Pipelines**. It opens `/schedules`. |
| 2 | Check the table. | Every schedule of P is listed, ADM's and ED's. Columns: Name, Type (agent / pipeline icon), Entity (name + version, link to the editor), Schedule (readable rule + timezone, cron in the tooltip), Next run, Last run (time + status), Owner, Active / Paused. |
| 3 | Check the status of each last run. | One label and icon per status: Running (spinner), Success, Awaiting approval, Failed, Blocked, Skipped. |
| 4 | Filter by **Type** = Agent, then Pipeline. | Only that type is listed. |
| 5 | Filter by **Status** = Success, Failed, Awaiting approval, then **Running** while a run is active (see ELITEA-4485). | Each filter lists only schedules whose last run has that status. **Running** keeps the schedule listed for the whole run, even when a cron tick is skipped meanwhile (#7435). |
| 6 | Filter by **Owner** = ED. | Only ED's schedule. |
| 7 | Search by part of a schedule name, then of an entity name. | Matching rows only; search ignores case. |
| 8 | Sort by **Next run** ascending, then descending. | Active schedules are in time order. **Paused schedules have no Next run and are grouped together** at one end. **Known bug #7421:** a paused schedule keeps its old Next run (sometimes a past time) and sorts among the active ones. |
| 9 | Sort by Name, Entity, Type, Last run, Active. | Each sort works in both directions. |
| 10 | With more than one page of schedules, page forward and back; change the page size. | Paging keeps filters and sort. |
| 11 | As ED, open Schedules. | Only ED's own schedule. No Owner filter for others' schedules. |
| 12 | As ED, open the URL of one of ADM's schedules. | "Schedule not found" (not a form with ADM's data). |
| 13 | As VW, open the navigation and `/schedules`. | No access: the item is hidden or the page shows no permission. |
| 14 | As ADM, open an agent schedule's entity link. | Opens the agent's editor in the same project mode. |

---

## Expected Final State

Each role sees exactly the schedules it may see; filters, search, sort and paging behave as above.

---

## Pass/Fail Criteria

**Pass:**
- Steps 1–14 behave as above (step 8 may fail only for the known bug #7421; step 5 Running may fail on 2.0.8 for #7435).

**Fail:**
- An editor sees another user's schedule, or a viewer can open the page.
- A filter, search or sort returns wrong rows.
