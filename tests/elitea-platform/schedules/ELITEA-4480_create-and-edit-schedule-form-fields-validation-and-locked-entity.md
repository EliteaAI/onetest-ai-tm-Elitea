---
id: ELITEA-4480
title: "Schedules — create and edit form: What to Run, Builder / Cron, timezone, stop date, approval rule, validation and locked entity"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:pipelines, issue:7011, issue:7338, issue:7439, issue:7425, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7338"]
---

# ELITEA-4480: Schedules — create and edit form: What to Run, Builder / Cron, timezone, stop date, approval rule, validation and locked entity

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the schedule form (two columns: Settings left, Runs right): General, What to Run, Schedule settings and Approval Rule. Check field rules, the error messages, the locked entity when the form opens from an agent / pipeline, the risk review at save and that Save stays off until something changes.

---

## Preconditions

- **Test data:** import [`qa-sch-agent-basic.agent.md`](../../../test-data/schedules/qa-sch-agent-basic.agent.md), [`qa-sch-agent-artifact.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.agent.md), [`qa-sch-pipeline-basic.pipeline.md`](../../../test-data/schedules/qa-sch-pipeline-basic.pipeline.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- A team project **P**; the tester is an editor or admin.
- An agent **AG** with two versions (**base** and **v2**), no sensitive tools.
- An agent **AG-S** whose toolkit has a tool on the Sensitive Action Tools list (e.g. Artifact `create_file`).
- A pipeline **PL** (Entry point capable) and a second agent **AG2**.

---

## Test Data

| Field | Value |
|-------|-------|
| Cron too frequent | `* * * * *`, `*/4 * * * *` |
| Cron invalid | `61 * * * *` |
| Timezone invalid | typed `Mars/Base` (if free text) |
| Stop date | yesterday; next month |
| Prompt with variables | "Summarise {{topic}} for {{team}}" |

---

## Steps

### Part A: from Schedules → New schedule

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Schedules → **New schedule**. | Two columns: **Settings** (General, What to Run, Schedule Settings, Approval Rule) and **Runs**. **Build with AI** is available. |
| 2 | What to Run: pick **Type** Agent, entity AG. | The **Version** dropdown preselects AG's default version; both versions are listed. |
| 3 | Type the prompt with `{{topic}}` and `{{team}}`. | A variable field appears for each placeholder. |
| 4 | Switch Type to **Pipeline**, pick PL. | **Run mode** appears: Entry point / Prompt, with the help "Entrypoint starts the pipeline from its entry point. Prompt sends the text below as the first message." Prompt is required only for Prompt mode. |
| 5 | Schedule Settings → **Builder**: pick weekdays at 09:00 and a timezone. | The readable rule matches; the **Cron Expression** tab shows the same cron. |
| 6 | **Cron Expression** tab: enter `* * * * *`, then `*/4 * * * *`. | Error "Runs must be at least 5 minutes apart". |
| 7 | Enter `61 * * * *`. | Error "invalid cron expression: … out of range". |
| 8 | Set **Stop on** = yesterday. | Error "The stop date is in the past". Next month is accepted. |
| 9 | Approval Rule. | Options **Pause and ask me** and **Run without asking** (same labels as the review dialog and the waiting cards, #7439), each with an ⓘ. "Run without asking" only when the project allows it. |
| 10 | Save with AG (no sensitive tool). | Saved; the schedule opens; Owner = the tester. |

### Part B: risk review and Save state

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | New schedule for **AG-S**, Save. | **Review risks before scheduling** lists 'Tool "create_file" of toolkit "<name>" needs approval' with badge and effect. Confirm → saved. |
| 12 | Open the saved AG-S schedule. | **Save is disabled** until a field changes; reverting the change disables it again. |
| 13 | Change only the **description** and Save. | The review asks again with the same tools: under "Pause and ask me" every save of a schedule with sensitive tools shows the review (accepted behaviour). Confirm → saved. |
| 14 | Try to change the **enabled** state from the form. | Not possible in the form; use Active / Paused (API returns "enabled cannot be changed by an edit; use the pause or resume action"). |

### Part C: from an agent / pipeline editor

| # | Action | Expected Result |
|---|--------|-----------------|
| 15 | Open AG's editor → Schedules section → **+ Schedule**. | The form opens with **Type and entity locked** to AG; version selectable. |
| 16 | Same from PL's editor. | Locked to PL; Run mode shown. |
| 17 | Through the API, create with AG2's version id and AG as the entity. | 400 "The version does not belong to this agent or pipeline". |
| 18 | Cancel on a changed form. | Unsaved-changes warning; Cancel leaves nothing saved. |

---

## Expected Final State

Two valid schedules exist (AG and AG-S); every invalid input was refused with a field message.

---

## Pass/Fail Criteria

**Pass:**
- All field rules and messages as above; the entity is locked from the editors; Save follows real changes.

**Fail:**
- An invalid cron, timezone, stop date or version is saved.
- The form opened from an editor lets the entity change.

