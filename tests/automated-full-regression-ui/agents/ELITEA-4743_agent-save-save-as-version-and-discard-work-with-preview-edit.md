---
id: ELITEA-4743
title: "Agent Save, Save As Version, and Discard work with the Preview/Edit Instructions editor"
priority: critical
type: regression
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4743: Agent Save, Save As Version, and Discard work with the Preview/Edit Instructions editor

**Module:** agents · **Priority:** critical · **Type:** regression

**Objective:** Verify that the existing agent versioning actions still work when Instructions are edited in the new Edit mode or viewed in Preview. Focus on what the issue changes: version switching in both modes with no stale content, and the active mode after Discard.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" is open, with no pending changes.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent | QA-7377 Agent |
| New version name | `v-7377` |
| Save edit text | `SAVE-7377` |
| Version edit text | `VERSION-7377` |
| Discard edit text | `DISCARD-7377` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch to Edit, add the line `SAVE-7377`, and click Save | Save completes. Save and Discard become disabled |
| 2 | Reload the page | `SAVE-7377` is shown in Preview, and in Edit after switching |
| 3 | In Edit, add `VERSION-7377`. Click Save As Version and name it `v-7377` | Version `v-7377` is created, selected, and shown in the VERSION dropdown with `VERSION-7377` in Instructions |
| 4 | Select `base` in the VERSION dropdown, first in Preview and then in Edit | `base` Instructions contain `SAVE-7377` but NOT `VERSION-7377`, in both modes |
| 5 | Select `v-7377`, first in Preview and then in Edit | `v-7377` Instructions contain `VERSION-7377` in both modes. No content from the other version is left over |
| 6 | In Edit, add `DISCARD-7377` and click Discard | The "Are you sure you want to discard changes?" dialog appears |
| 7 | Click Cancel | The dialog closes. `DISCARD-7377` is still in the editor, and Save and Discard are still enabled |
| 8 | Click Discard again and confirm | Content goes back to the saved value (no `DISCARD-7377`). Save and Discard become disabled |
| 9 | Write down which mode is active after Discard, then repeat steps 6 and 8 on skill "qa-7377-skill" | The agent and the skill end in the same mode after Discard (the current skill behavior is to stay in Edit) |

---

## Expected Final State

"QA-7377 Agent" has the `base` version (with `SAVE-7377`) and the `v-7377` version (with `VERSION-7377`). No discarded text is stored.

---

## Pass/Fail Criteria

**Pass:**
- Save, Save As Version and Discard work as before.
- Version switching shows the correct Instructions in both modes.
- The mode after Discard is the same for agents and skills.

**Fail:**
- Changes do not persist, the version shows content from another version, or Discard does not revert.
- The agent and the skill behave differently after Discard.

---

## Notes

- Also re-run the existing cases (not duplicated here): ELITEA-1888 (Save As Version), ELITEA-1890 (version switch updates fields), ELITEA-0098 (redirect to new version), ELITEA-4377 (Save/Save As Version/Discard for Editor and Admin), ELITEA-1871 (create/edit/discard lifecycle).
- Clean-up: delete version `v-7377` and remove `SAVE-7377` after the run.
- Manual source: ELITEA-4725 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4725_agent-save-save-as-version-and-discard-work-with-preview-edit.md`).
