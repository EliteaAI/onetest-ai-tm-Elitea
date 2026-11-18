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

**Objective:** Verify the agent versioning actions with the new Preview / Edit editor: switching versions shows the correct Instructions in both modes, with no content left over from another version; Discard → Cancel keeps the draft; and the INSTRUCTIONS section stays in Edit mode after Discard.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "Regression Instructions Agent" exists with the Instructions from Test Data. If it doesn't exist, create it with the Name, Description and Instructions from Test Data and click Save.
- The agent has no version named `regression-version` (delete it if it was left over from an earlier run).
- The `base` version of "Regression Instructions Agent" is open, with no pending changes.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent name | Regression Instructions Agent |
| Agent description | Regression agent for Instructions editor checks |
| Agent Instructions | `# Regression heading` (new line) `Base agent instructions.` |
| New version name | `regression-version` |
| Version edit text | `VERSION-MARKER` |
| Discard edit text | `DISCARD-MARKER` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch INSTRUCTIONS to Edit and add the line `VERSION-MARKER`. Click Save As Version and name it `regression-version` | Version `regression-version` is created, selected, and shown in the VERSION dropdown, with `VERSION-MARKER` in its Instructions |
| 2 | Select `base` in the VERSION dropdown. Check the Instructions in Preview, then in Edit | `base` Instructions do NOT contain `VERSION-MARKER`, in both modes |
| 3 | Select `regression-version`. Check the Instructions in Preview, then in Edit | `regression-version` Instructions contain `VERSION-MARKER` in both modes. No content from the other version is left over |
| 4 | In Edit, add `DISCARD-MARKER` and click Discard | The "Are you sure you want to discard changes?" dialog appears |
| 5 | Click Cancel | The dialog closes. `DISCARD-MARKER` is still in the editor, and Save and Discard are still enabled |
| 6 | Click Discard again and confirm | The content goes back to the saved value (no `DISCARD-MARKER`). Save and Discard become disabled. The INSTRUCTIONS section is still in Edit mode |
| 7 | Delete version `regression-version` | The version is removed from the VERSION dropdown |

---

## Expected Final State

"Regression Instructions Agent" has only its `base` version, unchanged. No discarded text is stored.

---

## Pass/Fail Criteria

**Pass:**
- Version switching shows the correct Instructions in both modes.
- Discard → Cancel keeps the draft, and Discard reverts it.
- The section stays in Edit mode after Discard.

**Fail:**
- A version shows content from another version, Save As Version fails, or Discard does not revert.
- The section switches to Preview after Discard.

---

## Notes

- Also re-run the existing cases (not duplicated here): ELITEA-1888 (Save As Version), ELITEA-1890 (version switch updates fields), ELITEA-0098 (redirect to new version), ELITEA-4377 (Save/Save As Version/Discard for Editor and Admin), ELITEA-1871 (create/edit/discard lifecycle, which covers plain Save).
- Skill equivalent: ELITEA-4747.
- Manual source: ELITEA-4725 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4725_agent-save-save-as-version-and-discard-work-with-preview-edit.md`).
