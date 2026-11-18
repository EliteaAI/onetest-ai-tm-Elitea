---
id: ELITEA-4740
title: "Saved agent Instructions open in Preview mode by default and render Markdown"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4740: Saved agent Instructions open in Preview mode by default and render Markdown

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Verify that the INSTRUCTIONS section of an existing, saved agent loads in Preview mode by default, renders formatted Markdown, and shows a labeled Preview | Edit switch.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role in the project.
- Agent "QA-7377 Agent" exists and is saved. Its Instructions contain an H1/H2 heading, a numbered list, a bullet list, **bold**, `inline code`, a fenced code block, a link, a table, and a `{{user_input}}` variable reference.
- At least one other saved agent exists in the same project.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent | QA-7377 Agent |
| Second agent | Any other saved agent in the project |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Agents and open "QA-7377 Agent" | The agent details page loads without errors |
| 2 | Scroll to the INSTRUCTIONS section without clicking in it | The Preview / Edit switch is visible. Preview is the active option (in DevTools, "Preview mode" has `aria-pressed="true"` and "Edit mode" has `aria-pressed="false"`) |
| 3 | Check how the Instructions content is shown | The heading, numbered list, bullet list, bold text, inline code, fenced code block, link and table are shown as formatted content. No raw Markdown symbols (`#`, `**`, `` ``` ``, `|---|`) are visible |
| 4 | Click the link in the rendered Instructions | The link behaves as a normal link (opens the target) and does not switch the section to Edit or change the content |
| 5 | Reload the page (F5) | The agent reloads with Preview active and the same rendered content |
| 6 | Open the second agent, then go back to "QA-7377 Agent" | "QA-7377 Agent" opens with Preview active |
| 7 | Open the browser console | No errors related to the Instructions editor or Markdown rendering |

---

## Expected Final State

"QA-7377 Agent" is unchanged and is shown in Preview mode with rendered Markdown every time it is opened.

---

## Pass/Fail Criteria

**Pass:**
- Saved agents always open with Preview active in the INSTRUCTIONS section.
- All listed Markdown structures render as formatted content.

**Fail:**
- The saved agent opens in Edit mode, or with no Preview / Edit switch.
- Raw Markdown is shown in Preview, rendering is broken, or console errors appear.

---

## Notes

- New, unsaved agents open in Edit mode by default (QA owner clarification, 2026-11-17). See ELITEA-4741.
- Manual source: ELITEA-4722 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4722_saved-agent-instructions-open-in-preview-mode-and-render-markdown.md`).
