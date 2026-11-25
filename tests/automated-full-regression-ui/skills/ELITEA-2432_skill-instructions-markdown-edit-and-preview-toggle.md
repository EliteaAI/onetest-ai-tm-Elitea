---
id: ELITEA-2432
title: "Skill and agent instructions — Markdown edit and preview toggle"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-2432: Skill and agent instructions — Markdown edit and preview toggle

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify the shared Instructions Preview / Edit toggle on Skills and Agents. A saved Skill or Agent opens in Preview with rendered Markdown. A new, unsaved Agent opens in Edit. Copy to clipboard is shown only in Edit (on Agents, Full Screen too; Skills have no Full Screen for the instructions), and Collapse field is not shown in either mode. Edits switch cleanly between modes and persist after save and re-open.

---

## Preconditions

- User is logged in to the Elitea platform with the Admin or Editor role.
- One saved Skill and one saved Agent exist in the project, with no pending changes.
- The user has permission to create Agents.

---

## Test Data

| Field | Value |
|-------|-------|
| Markdown to append | `## Toggle check` (new line) `- **bold item**` (new line) `` `inline code` `` |
| Entities | Saved Skill; saved Agent |
| New-agent Instructions | `# Draft toggle` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the saved Skill and go to the INSTRUCTIONS section | The section opens in Preview mode. The Markdown body is rendered as formatted content, not raw Markdown, and the frontmatter block is not shown |
| 2 | In Preview, hover over the Instructions content and header | Only the Preview / Edit switch is shown. No Copy to clipboard, Full screen view or Collapse field icon appears |
| 3 | Switch to Edit mode | The raw Markdown source is shown in the editor with line numbers. Copy to clipboard is shown left of Test. There is no Full Screen button for the instructions, and no Collapse field / Expand field control |
| 4 | Append the Markdown from the Test Data table | The text is added. Save becomes enabled |
| 5 | Switch to Preview mode and check the rendered output | "Toggle check" is shown as a heading, "bold item" as a bold list item, and "inline code" as code |
| 6 | Switch back to Edit mode | The raw Markdown matches exactly what was typed |
| 7 | Save, then re-open the Skill | The Skill opens in Preview. The updated instructions persist and render correctly |
| 8 | Repeat steps 1–7 on the saved Agent | The Agent behaves the same as the Skill, except that in step 3 Full Screen is also available (in step 1, the Agent has no frontmatter to hide) |
| 9 | Go to Agents and click + Agent (a new, unsaved agent). Go to INSTRUCTIONS without clicking in it | The section opens in Edit mode, and typing `# Draft toggle` works right away. Switching to Preview renders it as a heading |
| 10 | Leave the new agent without saving (discard if asked) | No new agent is created |

---

## Expected Final State

The saved Skill and the saved Agent contain the appended Markdown and open in Preview. No unsaved agent is created.

---

## Pass/Fail Criteria

**Pass:**
- Saved Skills and Agents open in Preview with rendered Markdown, and a new, unsaved Agent opens in Edit.
- Copy to clipboard (and, on Agents, Full Screen) appears only in Edit. Skills show no Full Screen for the instructions. Collapse field appears in neither mode.
- Edits are kept exactly across mode switches and persist after save and re-open.

**Fail:**
- The wrong default mode is used, raw Markdown is shown in Preview, or the frontmatter is shown in Preview.
- Editor action icons appear in Preview, or Collapse field is still present.
- Content is lost or changed when switching modes, or does not persist after save.

---

## Notes

- Updated for EliteaAI/elitea_issues#7377 (unified Agent and Skill Instructions Preview / Edit modes). Default-mode rule (QA owner clarification, 2026-11-17): a new, unsaved Agent opens in Edit; a saved Agent or Skill opens in Preview.
- Detailed functional coverage: ELITEA-4722 to ELITEA-4739 (`tests/elitea-platform/agents/instructions-preview-edit/`).
- Updated for EliteaAI/elitea_issues#7573: the skill page no longer has Full Screen for the instructions.
