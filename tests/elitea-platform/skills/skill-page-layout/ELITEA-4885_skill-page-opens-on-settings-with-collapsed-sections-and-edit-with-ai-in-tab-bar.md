---
id: ELITEA-4885
title: "Skill page opens on Settings with General left, Instructions right, collapsed sections and Edit with AI in the tab bar"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4885: Skill page opens on Settings with General left, Instructions right, collapsed sections and Edit with AI in the tab bar

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify the default layout of the skill page: the Settings tab is active, General is on the left and Instructions (SKILL.md) on the right, Run settings and Information are collapsed, and Edit with AI is at the right end of the Settings / Files tab bar and works as before.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill A `layout-skill` exists and is saved, with the Instructions and files from Test Data. If the files are missing, add them in **Files → +** (Add files).
- Skill B `layout-skill-empty` exists and is saved, with no files.
- The browser window is at least 1366 × 768 px, unless a step says otherwise.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Skill A | `layout-skill` |
| Skill A files | `references/guide.md` (text, 3 lines), `scripts/run.py` (text), `assets/logo.png` (binary), `README.txt` (root) |
| Skill B | `layout-skill-empty` (no files) |
| Marker | `LAYOUT-MARKER` |

Skill A Instructions body:

~~~markdown
# Layout test skill

See references/guide.md for details.
Run scripts/run.py when needed.
Open [the guide](references/guide.md).

Reply with LAYOUT-OK.
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Skill A from the Skills list | The `Settings` tab is active. The tab bar shows `Settings` and `Files – 4`. The left column shows `GENERAL` expanded (Name, Description, Tags). The right column has the header "Instructions (SKILL.md)" |
| 2 | Check `RUN SETTINGS` and `INFORMATION`, then click each of them | Both are collapsed when the page opens. Expanded, Run settings shows "Include project context", and Information shows Skill ID and Version ID |
| 3 | Check the right end of the tab bar | `Edit with AI` is there, styled as before. It is not in the top toolbar |
| 4 | Click `Edit with AI`, then `Cancel` | The Edit with AI panel opens with `Generate Draft` and `Cancel`. After Cancel the skill is unchanged |

---

## Expected Final State

Skill A is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Settings opens by default with the two zones and the collapsed sections.
- Edit with AI is in the tab bar and opens its panel.

**Fail:**
- Another tab opens by default, the zones are swapped or missing, or Run settings / Information are expanded.
- Edit with AI is missing, placed elsewhere, or does not open.

---

## Notes

- Covers AC1, AC2 of EliteaAI/elitea_issues#7573.
- The full Edit with AI flow is covered by ELITEA-2611 and ELITEA-2613.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
