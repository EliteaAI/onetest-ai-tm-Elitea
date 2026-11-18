---
id: ELITEA-4746
title: "Switching Preview and Edit preserves unsaved skill changes without auto-saving"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4746: Switching Preview and Edit preserves unsaved skill changes without auto-saving

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that switching the skill INSTRUCTIONS between Preview and Edit keeps the draft (frontmatter and body) and the character counter, never saves automatically, and that the unsaved-changes warning appears both on page reload and on version switch.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Skill "regression-instructions-skill" exists with the Name, Description and Instructions body from Test Data. If it doesn't exist, create it with those values and click Save.
- The skill has a second version named `regression-v2`. If it doesn't exist, open the skill and click Save As Version with the name `regression-v2`.
- The `base` version of "regression-instructions-skill" is open, with no pending changes (Save and Discard are disabled).

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill name | regression-instructions-skill |
| Skill description | Regression skill for Instructions editor checks |
| Second version | `regression-v2` |
| Appended text | `## Added section REGRESSION-MARKER` (new line) `- new bullet item` |

Instructions body (used only when the skill has to be created):

~~~markdown
# Skill regression heading
1. First step
- **Bold item** with `inline code`
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In INSTRUCTIONS, switch to Edit. Write down the "characters left" value | The frontmatter block (`name: regression-instructions-skill`, `description: …`) and the raw body are shown. The counter is visible |
| 2 | Append the test text at the end of the body | The text is added. Save and Discard become enabled. The counter goes down |
| 3 | Switch to Preview | "Added section REGRESSION-MARKER" is shown as a heading and "new bullet item" as a list item. The frontmatter block is not shown. Save and Discard are still enabled |
| 4 | Switch back to Edit | The frontmatter and the body match exactly what was there before, including the appended text. The counter shows the same value as after step 2 |
| 5 | Switch Preview ↔ Edit 5 times quickly | The content and the counter are unchanged, and nothing is duplicated. No errors appear |
| 6 | Reload the page (F5) | An unsaved-changes warning appears. Choose to stay on the page: the draft with "REGRESSION-MARKER" is still in the editor |
| 7 | In the VERSION dropdown, select `regression-v2` | An unsaved-changes warning appears. Choose to stay: the `base` version is still open, and the draft with "REGRESSION-MARKER" is still in the editor |
| 8 | Select `regression-v2` again and, in the warning, choose to leave without saving. Then select `base` | `regression-v2` opens. When `base` opens again, its Instructions do NOT contain "REGRESSION-MARKER", which shows that switching modes did not save |
| 9 | Make the same edit again and click Save | Save completes. Save and Discard become disabled |
| 10 | Reload the page; check Preview, then Edit | The change is shown in both modes. The frontmatter is hidden in Preview and shown unchanged in Edit |

---

## Expected Final State

The `base` version of "regression-instructions-skill" contains the appended section only after the explicit Save in step 9. Remove the appended section after the run.

---

## Pass/Fail Criteria

**Pass:**
- Mode switches keep the frontmatter, the body and the counter exactly as they were. Preview shows unsaved edits with the frontmatter hidden.
- The unsaved-changes warning appears both on reload and on version switch.
- No save happens without clicking Save.

**Fail:**
- Content or frontmatter is lost, duplicated or changed when modes are switched, or the counter changes.
- The warning is missing on reload or on version switch.
- Switching modes saves the skill, or turns off the unsaved-changes state.

---

## Notes

- Mirrors agent regression case ELITEA-4742.
- Not duplicated here: the basic toggle and save-and-reopen flow (ELITEA-2432).
- Clean-up: remove the appended section after the run.
