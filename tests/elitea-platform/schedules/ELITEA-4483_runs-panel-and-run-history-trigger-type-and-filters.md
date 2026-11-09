---
id: ELITEA-4483
title: "Schedules — Runs (count) panel and Run History: Trigger type, filters by schedule, status, trigger and version"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:pipelines, issue:7338, issue:7011, issue:7270, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7338", "EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7270"]
---

# ELITEA-4483: Schedules — Runs (count) panel and Run History: Trigger type, filters by schedule, status, trigger and version

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify the **Runs (count)** panel on a schedule (newest first, Latest indicator, one expanded card, content by status, Open in Run History) and the agent / pipeline **Run History**: the **Trigger type** column (Scheduled, Manual, Test) and the filter bar (Schedule, Status, Trigger type, Version). Also the breadcrumb from a schedule run (#7270).

---

## Preconditions

- A schedule **S** for agent **AG** with several runs: a cron run (Success), a Run Now (Manual, Failed), a run Awaiting approval, a Skipped run (cron overlap), and runs of two versions.
- A test run of AG (ELITEA-4482).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open S → **Runs (count)**. | Count matches; newest first; the newest has **Latest**. Each card: time, trigger, version, duration, tokens / cost when known, status. |
| 2 | Expand a Success run, then a Failed run. | Only one card is expanded at a time. Failed shows the reason (short, no traceback); "Run logs" / "Hide run logs" toggles the log. |
| 3 | Expand the Awaiting approval run. | The waiting card with Approve / Reject (see ELITEA-4457). |
| 4 | Expand the Skipped run. | Reason "the previous run is still running". |
| 5 | **Open in Run History** on a card. | Run History opens on that run. |
| 6 | The breadcrumb Agent / Pipeline in that view. | Opens the entity in the same project, not a public route (#7270). |
| 7 | AG → Run History. Check the **Trigger type** column. | Scheduled (cron), Manual (Run Now), Test (test run). No "All schedules" option. |
| 8 | Filter **Schedule** = S. | Only S's runs. |
| 9 | Filter **Status** = Failed, then Awaiting approval, then Running during a run. | Matching runs only. |
| 10 | Filter **Trigger type** = Scheduled / Manual / Test. | Matching runs only. |
| 11 | Filter **Version** = v2. | Only runs of v2. |
| 12 | Combine Schedule + Status + Version. | All filters apply together; clearing one updates the list. |
| 13 | Same on a pipeline's Run History. | Same behaviour. |

---

## Expected Final State

No change to data; the views show the runs as above.

---

## Pass/Fail Criteria

**Pass:**
- Panel and Run History behave as above.

**Fail:**
- Wrong trigger type, a filter returns wrong runs, or the breadcrumb opens a wrong route.
