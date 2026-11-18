---
id: ELITEA-4745
title: "Skill Instructions default mode: new unsaved skill opens in Edit, saved skill opens in Preview"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4745: Skill Instructions default mode: new unsaved skill opens in Edit, saved skill opens in Preview

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify the default mode of the skill INSTRUCTIONS section. A new, unsaved skill opens in Edit with the frontmatter block and the character counter visible. After the first Save, the skill opens in Preview with the frontmatter hidden, and it stays in Preview after a reload and after leaving and coming back.

---

## Preconditions

- User is logged in to `{{base_url}}` and has permission to create skills in the project.
- No skill named "regression-new-skill" exists in the project (delete it if it was left over from an earlier run).
- At least one other saved skill exists in the project. If none exists, create "regression-other-skill" with a Name, Description and one line of Instructions.
- The browser DevTools console is open.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Name | regression-new-skill |
| Description | Regression skill for Instructions default mode |
| Second skill | Any other saved skill (or "regression-other-skill") |

Instructions body to type below the frontmatter block:

~~~markdown
# Skill regression heading
1. First step
- **Bold item** with `inline code`
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Skills and click + Skill (Create Skill) | The new skill form opens |
| 2 | Scroll to the INSTRUCTIONS section without clicking in it | The Preview / Edit switch is visible and Edit is the active option ("Edit mode" has `aria-pressed="true"`). The editor shows an empty frontmatter block with `name:` and `description:` keys, and a "characters left" counter is shown |
| 3 | Click in the editor below the frontmatter block and type the body from Test Data | The text appears as typed, with no extra click or mode change. The "characters left" counter goes down as you type |
| 4 | Switch to Preview | The body renders as formatted content (heading, numbered item, bold text, inline code). The frontmatter block is not shown. Nothing is saved: the skill does not appear in the Skills list |
| 5 | Switch back to Edit | The frontmatter block and the body are shown exactly as before. The counter shows the same value as in step 3 |
| 6 | Enter the Name and Description from Test Data, then click Save | The skill is created. The frontmatter `name:` and `description:` show the saved values |
| 7 | Reload the page (F5) | The saved skill opens with Preview active. The body is rendered and the frontmatter block is not shown |
| 8 | Open the second skill, then go back to "regression-new-skill" | "regression-new-skill" opens with Preview active |
| 9 | Check the browser console | No errors related to the Instructions editor or Markdown rendering |
| 10 | Delete "regression-new-skill" | The skill is removed from the Skills list |

---

## Expected Final State

No test skills are left in the project (except "regression-other-skill", if it was created).

---

## Pass/Fail Criteria

**Pass:**
- A new, unsaved skill opens Instructions in Edit, with the frontmatter block and the counter visible.
- After the first Save, the skill opens in Preview with the frontmatter hidden, after a reload and after leaving and coming back.

**Fail:**
- A new skill opens in Preview, or the user must click before typing is possible.
- A saved skill opens in Edit, or the frontmatter is shown in Preview.
- Switching modes before the first save loses text, changes the counter, or saves the skill.

---

## Notes

- Mirrors agent regression case ELITEA-4741.
- New-skill default mode = Edit (consistent with ELITEA-4276 step 2: the create form opens the editor with an empty frontmatter block).
- Not duplicated here: saved-skill Markdown rendering, the toggle icons and Collapse field (ELITEA-2432); frontmatter ⇄ field sync (ELITEA-4658); the 50,000-character limit (ELITEA-1992 and the manual case ELITEA-4205).
