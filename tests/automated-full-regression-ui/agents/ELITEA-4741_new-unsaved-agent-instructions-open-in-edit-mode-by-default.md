---
id: ELITEA-4741
title: "Agent Instructions default mode: new unsaved agent opens in Edit, saved agent opens in Preview"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4741: Agent Instructions default mode: new unsaved agent opens in Edit, saved agent opens in Preview

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Verify the default mode of the agent INSTRUCTIONS section. A new, unsaved agent opens in Edit, so the user can type right away. After the first Save, the agent opens in Preview with rendered Markdown, and it stays in Preview after a reload and after leaving and coming back.

---

## Preconditions

- User is logged in to `{{base_url}}` and has permission to create agents in the project.
- No agent named "Regression New Agent" exists in the project (delete it if it was left over from an earlier run).
- At least one other saved agent exists in the project. If none exists, create "Regression Other Agent" with Name and Description only.
- The browser DevTools console is open.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Name | Regression New Agent |
| Description | Regression agent for Instructions default mode |
| Instructions | The Markdown block below |
| Second agent | Any other saved agent (or "Regression Other Agent") |

Instructions to type:

~~~markdown
# Regression heading
## Rules
1. First rule
2. Second rule

- Bullet item
- **Bold item** with `inline code`

```text
fenced code line
```

[ELITEA](https://elitea.ai)

| Col A | Col B |
|-------|-------|
| a1    | b1    |
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Agents and click + Agent | The new agent form opens |
| 2 | Scroll to the INSTRUCTIONS section without clicking in it | The Preview / Edit switch is visible. Edit is the active option ("Edit mode" has `aria-pressed="true"`, "Preview mode" has `aria-pressed="false"`) |
| 3 | Click in the Instructions editor and type the Instructions from Test Data | The text appears as typed. No mode change or extra click is needed first |
| 4 | Switch to Preview | The headings, numbered list, bullet list, bold text, inline code, fenced code block, link and table are shown as formatted content, with no raw Markdown symbols. Nothing is saved: the agent does not appear in the Agents list |
| 5 | Switch back to Edit | The raw Markdown is exactly what was typed |
| 6 | Enter the Name and Description from Test Data, then click Save | The agent is created with the typed Instructions |
| 7 | Reload the page (F5) | The saved agent opens with Preview active ("Preview mode" has `aria-pressed="true"`), and the Instructions are rendered as in step 4 |
| 8 | Click the link in the rendered Instructions | The link opens its target as a normal link. The section does not switch to Edit, and the content does not change |
| 9 | Open the second agent, then go back to "Regression New Agent" | "Regression New Agent" opens with Preview active |
| 10 | Open Chat, start a conversation, and create a new agent from the conversation canvas. Go to INSTRUCTIONS without clicking in it, then close the canvas without saving | Edit is the active option in the canvas. No agent is created |
| 11 | Check the browser console | No errors related to the Instructions editor or Markdown rendering |
| 12 | Delete "Regression New Agent" | The agent is removed from the Agents list |

---

## Expected Final State

No test agents are left in the project (except "Regression Other Agent", if it was created).

---

## Pass/Fail Criteria

**Pass:**
- Every new, unsaved agent (Agents → + Agent, and Chat canvas) opens Instructions in Edit mode.
- After the first Save, the agent opens in Preview with rendered Markdown, after a reload and after leaving and coming back.

**Fail:**
- A new agent opens in Preview, or the user must click before typing is possible.
- A saved agent opens in Edit, or raw Markdown is shown in Preview.
- Switching modes before the first save loses text or saves the agent, or console errors appear.

---

## Notes

- Decision source: QA owner clarification, 2026-11-17 (new unsaved agent opens in Edit; saved agents open in Preview).
- Skill equivalent: ELITEA-4745.
- Related: ELITEA-1871 (agent create validation), ELITEA-1920 (Build with AI in chat agent editor).
- Merged from the former regression copy of ELITEA-4722 (saved agent opens in Preview): steps 7–9 and 11.
- Manual source: ELITEA-4723 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4723_new-unsaved-agent-instructions-open-in-edit-mode-by-default.md`).
- Manual source: ELITEA-4722 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4722_saved-agent-instructions-open-in-preview-mode-and-render-markdown.md`).
