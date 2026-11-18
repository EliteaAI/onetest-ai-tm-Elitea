---
id: ELITEA-4729
title: "Copy to clipboard in Edit mode copies the current Instructions draft (agents and skills)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4729: Copy to clipboard in Edit mode copies the current Instructions draft (agents and skills)

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that Copy to clipboard is shown in Edit mode and copies the full current editor source as raw Markdown, including unsaved edits and frontmatter.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Browser clipboard permission is granted for the ELITEA origin.
- An external text editor (for example, Notepad) is open.

---

## Test Data

| Entity | Content expected in the pasted text |
|---|---|
| Agent "QA-7377 Agent" | Full Markdown source + `COPY-PROBE-7377` (+ frontmatter, if agent frontmatter is implemented) |
| Skill "qa-7377-skill" | `---` frontmatter block with name/description + full Markdown body + `COPY-PROBE-7377` |
| Agent "QA-7377 Empty" | Empty content (no probe line added); no error |
| Agent "QA-7377 Large" (~40,000 characters) | Full source, not truncated |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the first entity from the Test Data table and switch INSTRUCTIONS to Edit | The Copy to clipboard button is visible |
| 2 | Hover the Copy to clipboard button | The tooltip "Copy to clipboard" is shown. In DevTools, the button has an accessible name (`aria-label` or similar) |
| 3 | Add the unsaved line `COPY-PROBE-7377` (skip this for "QA-7377 Empty" and "QA-7377 Large") and click Copy to clipboard | Success feedback appears (a toast or an icon change) |
| 4 | Paste into the external text editor | The pasted text matches the "Content expected" column. It is raw Markdown (not rendered HTML), line breaks are kept, and nothing is cut off |
| 5 | Repeat steps 1–4 for every other row in the Test Data table | Every row passes |
| 6 | Discard the unsaved changes on each entity | The entities are unchanged |

---

## Expected Final State

No entity is changed. The clipboard holds the last copied source.

---

## Pass/Fail Criteria

**Pass:**
- The copied text is exactly the current editor source, including unsaved edits and frontmatter.
- Copy feedback and the tooltip are shown, and the button has an accessible name.

**Fail:**
- The copy uses the saved value instead of the draft, includes HTML, is cut off, or loses line breaks.
- Copying empty Instructions shows an error, or the button has no accessible name.

---

## Notes

- At authoring time, the agent copy button had no `aria-label`.
- Re-run ELITEA-3322 and ELITEA-3337 (Copy in the Compare Versions modal), which share the editor components.
