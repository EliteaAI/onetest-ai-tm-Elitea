---
id: ELITEA-4748
title: "Viewer role keeps skill Instructions read-only in Preview and Edit"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4748: Viewer role keeps skill Instructions read-only in Preview and Edit

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that a Viewer cannot change skill Instructions (body or frontmatter) through the new Edit mode or Full Screen, while still being able to read and copy them.

---

## Preconditions

- A Viewer user (User B) exists in a shared project that contains the test skill. User A has the Admin or Editor role in the same shared project.
- The test skill is created in the shared project by User A: if skill "regression-instructions-skill" doesn't exist there, User A creates it in the shared project with the Name, Description and Instructions body from Test Data and clicks Save.
- An external text editor (for example, Notepad) is open.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill name | regression-instructions-skill |
| Skill description | Regression skill for Instructions editor checks |
| Instructions body | `# Skill regression heading` (new line) `Base skill instructions.` |
| Typing probe | `READONLY-MARKER` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User B and open "regression-instructions-skill" | The INSTRUCTIONS section renders the body in Preview. The frontmatter block is not shown |
| 2 | If an Edit switch is offered, switch to Edit | Either no Edit switch is offered, or Edit shows the frontmatter block and the body as read-only |
| 3 | Try to type `READONLY-MARKER` in the body, paste text, and delete text. Then try to change `name:` in the frontmatter | Nothing changes. The Name and Description fields are unchanged |
| 4 | Check the page actions | Save, Save As Version and Discard are hidden or disabled |
| 5 | Click Copy to clipboard (in Edit mode, if the switch is offered) and paste into the external text editor | Copy to clipboard is available. The pasted text matches the skill Instructions (in Edit mode, including the frontmatter block) |
| 6 | Open Full Screen (if available) and try to type `READONLY-MARKER` | Full Screen opens read-only. No edit is possible |
| 7 | Log in as User A and open "regression-instructions-skill" | The Instructions do not contain `READONLY-MARKER`, and the skill is unchanged |

---

## Expected Final State

"regression-instructions-skill" is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- The Viewer cannot change the body or the frontmatter through inline Edit or Full Screen, and save actions are not available.
- The Viewer can copy the Instructions.

**Fail:**
- Any text or frontmatter can be changed, or Save / Save As Version / Discard becomes available.
- Copy to clipboard is missing for the Viewer, or the pasted text does not match.

---

## Notes

- Mirrors agent regression case ELITEA-4744, Part A. The published skill version block stays in ELITEA-4744, Part B, and is not duplicated here.
- Not duplicated here: Edit with AI hidden for Viewer (ELITEA-2613), and Save / Save As Version / Discard hidden for Viewer on skill details (manual case ELITEA-4376).
