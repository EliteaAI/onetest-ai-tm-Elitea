---
id: ELITEA-4963
title: "Agent and Pipeline compare versions keep Save under each field and use the new bottom bar"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4963: Agent and Pipeline compare versions keep Save under each field and use the new bottom bar

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that the compare components shared with skills still work for Agents and Pipelines: no Files step, new bottom bar and header, per-field Save and the discard warning.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- An agent and a pipeline each have at least 2 versions with different Instructions / text fields.

---

## Test Data

| Field | Value |
|-------|-------|
| Agents | `{{base_url}}/app/agents/all` |
| Pipelines | `{{base_url}}/app/pipelines/all` |
| Edit text | `QA-7675` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent → actions menu → **Compare versions**, choose two versions, **Compare**. | Modal opens; no Files step. |
| 2 | Step through all steps. | **← Select versions** on the left; Next / Previous / Finish on the right; header meta in normal case; no Save in headers. |
| 3 | Edit the second version's Welcome message to `QA-7675` and click the Save under that field. | Success toast; only that field of that version is saved. |
| 4 | Make another unsaved edit, click **← Select versions**. | Discard warning appears; confirm discard. |
| 5 | Repeat steps 1–4 for the pipeline (edit any editable text field). | Same behaviour; the edit is saved only to the chosen pipeline version. |
| 6 | Check DevTools Console. | No errors from the compare modal. |

---

## Expected Final State

Only the edited agent and pipeline versions have `QA-7675`.

---

## Pass/Fail Criteria

**Pass:**
- Agent and Pipeline compare open, save per field and show the new bottom bar.

**Fail:**
- Header Save or Files step appears for agents/pipelines.
- Per-field Save missing or saves the wrong version.
