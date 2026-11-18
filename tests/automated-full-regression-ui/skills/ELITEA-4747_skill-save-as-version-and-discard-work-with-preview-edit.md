---
id: ELITEA-4747
title: "Skill Save As Version, version switching, and Discard work with the Preview/Edit Instructions editor"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4747: Skill Save As Version, version switching, and Discard work with the Preview/Edit Instructions editor

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify the skill versioning actions with the Preview / Edit editor: Save As Version from Edit mode; switching versions shows the correct body and frontmatter in both modes, with no content left over; Discard → Cancel keeps the draft; and the INSTRUCTIONS section stays in Edit mode after Discard.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Skill "regression-instructions-skill" exists with the Name, Description and Instructions body from Test Data. If it doesn't exist, create it with those values and click Save.
- The skill has no version named `regression-version` (delete it if it was left over from an earlier run).
- The `base` version of "regression-instructions-skill" is open, with no pending changes.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill name | regression-instructions-skill |
| Skill description | Regression skill for Instructions editor checks |
| Instructions body | `# Skill regression heading` (new line) `Base skill instructions.` |
| New version name | `regression-version` |
| Version edit text | `VERSION-MARKER` |
| Discard edit text | `DISCARD-MARKER` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch INSTRUCTIONS to Edit and add the line `VERSION-MARKER` to the body. Click Save As Version and name it `regression-version` | Version `regression-version` is created, selected, and shown in the VERSION dropdown, with `VERSION-MARKER` in its body |
| 2 | Select `base` in the VERSION dropdown. Check the Instructions in Preview, then in Edit | `base` does NOT contain `VERSION-MARKER` in either mode. The frontmatter is hidden in Preview and shown in Edit with `name: regression-instructions-skill` |
| 3 | Select `regression-version`. Check the Instructions in Preview, then in Edit | `regression-version` contains `VERSION-MARKER` in both modes. The frontmatter is hidden in Preview and shown in Edit. No content from the other version is left over |
| 4 | In Edit, add `DISCARD-MARKER` to the body and click Discard | The "Are you sure you want to discard changes?" dialog appears |
| 5 | Click Cancel | The dialog closes. `DISCARD-MARKER` is still in the editor, and Save and Discard are still enabled |
| 6 | Click Discard again and confirm | The body goes back to the saved value (no `DISCARD-MARKER`), and the frontmatter is unchanged. Save and Discard become disabled. The INSTRUCTIONS section is still in Edit mode |
| 7 | Delete version `regression-version` | The version is removed from the VERSION dropdown |

---

## Expected Final State

"regression-instructions-skill" has only its `base` version, unchanged. No discarded text is stored.

---

## Pass/Fail Criteria

**Pass:**
- Save As Version works from Edit mode, and version switching shows the correct body and frontmatter in both modes.
- Discard → Cancel keeps the draft, and Discard reverts it.
- The section stays in Edit mode after Discard.

**Fail:**
- A version shows content from another version, or the frontmatter appears in Preview.
- Discard does not revert, or changes the frontmatter.
- The section switches to Preview after Discard.

---

## Notes

- Mirrors agent regression case ELITEA-4743.
- Not duplicated here: plain Save and reopen (ELITEA-2428, ELITEA-2432), the version comparison modal (ELITEA-3352), the test panel using the selected version (ELITEA-2440), and frontmatter rename across versions (ELITEA-4658).
