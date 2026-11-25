---
id: ELITEA-4890
title: "On Files the Instructions panel has Copy next to close, and SKILL.md links open files with the mentioning lines highlighted"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4890: On Files the Instructions panel has Copy next to close, and SKILL.md links open files with the mentioning lines highlighted

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that on the Files tab the Instructions panel header has Copy next to ✕ behind a divider, the lines of SKILL.md that mention the open file are highlighted, and links to files in SKILL.md open the file in Files (Ctrl-click in code mode, plain click on a Markdown link in preview).

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
| 1 | Open Skill A → `Files – 4`, click `guide.md`, then `Instructions` | The Instructions open as a third column in code mode. The header has Copy, a divider and ✕ ("Close the instructions"). The URL gets `panel=instructions` |
| 2 | Check the Instructions | The line `See references/guide.md for details.` is highlighted |
| 3 | Click Copy and paste the clipboard | The whole SKILL.md source is pasted |
| 4 | In the panel, plain-click `scripts/run.py`, then Ctrl-click it (⌘-click on macOS) | A plain click does not navigate. Ctrl-click opens `run.py`, and the highlight moves to `Run scripts/run.py when needed.` |
| 5 | Open `Settings`. In preview, click the link "the guide" | The Files tab opens with `guide.md` |

---

## Expected Final State

Skill A is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Copy, divider and ✕ in the Files Instructions header; Copy copies the whole source.
- Mentioning lines highlighted; links open the file.

**Fail:**
- Copy missing or placed elsewhere.
- No highlight, or a link does not open the file.

---

## Notes

- Covers AC5, AC11 of EliteaAI/elitea_issues#7573.
- In preview a plain path is plain text; only a Markdown link opens the file. In code mode a plain click places the cursor and Ctrl-click (⌘-click) opens the file.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
