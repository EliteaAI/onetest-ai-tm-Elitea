---
id: ELITEA-4741
title: "New unsaved agent Instructions open in Edit mode by default"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4741: New unsaved agent Instructions open in Edit mode by default

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Verify that the Instructions section of a new agent that has not been saved yet opens in Edit mode, so the user can type immediately. Also verify that the Preview / Edit switch works before the first save, and that the agent opens in Preview after the first Save and a reload.

---

## Preconditions

- User is logged in to `{{base_url}}` and has permission to create agents in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Instructions typed | `# Draft 7377` (new line) `- first bullet` |
| Name | QA-7377 New Agent |
| Description | Created by ELITEA-4741 |

| Entry point (unsaved agent) | Expected default mode |
|---|---|
| Agents → + Agent | Edit |
| Chat → create agent from the conversation canvas / agent editor | Edit |
| Build with AI (only if it shows the Instructions editor before the agent is created) | Edit |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Agents and click + Agent | The new agent form opens |
| 2 | Scroll to the INSTRUCTIONS section without clicking in it | The Preview / Edit switch is visible. Edit is the active option ("Edit mode" has `aria-pressed="true"`, "Preview mode" has `aria-pressed="false"`) |
| 3 | Click in the Instructions editor and type the test Instructions | The text appears as typed. No mode change or extra click is needed first |
| 4 | Switch to Preview | "Draft 7377" is shown as a heading and "first bullet" as a list item. Nothing is saved: the agent does not appear in the Agents list |
| 5 | Switch back to Edit | The raw Markdown is exactly what was typed |
| 6 | Enter Name and Description, then click Save | The agent is created with the typed Instructions |
| 7 | Reload the page (F5) | The saved agent opens with Preview active and the Instructions rendered |
| 8 | Repeat steps 2–5 for each other entry point in the Test Data table | Each unsaved agent opens Instructions in Edit, and the switch works the same way |

---

## Expected Final State

Agent "QA-7377 New Agent" exists with the typed Instructions and opens in Preview. Unsaved agents created from the other entry points are not saved.

---

## Pass/Fail Criteria

**Pass:**
- Every new, unsaved agent opens Instructions in Edit mode.
- After the first Save and a reload, the agent opens in Preview.

**Fail:**
- A new agent opens in Preview, or the user must click before typing is possible.
- Switching modes before the first save loses text or saves the agent.

---

## Notes

- Decision source: QA owner clarification, 2026-11-17 (new unsaved agent opens in Edit; saved agents open in Preview).
- Related: ELITEA-1871 (agent create validation), ELITEA-1920 (Build with AI in chat agent editor).
- Clean-up: delete "QA-7377 New Agent" after the run.
- Manual source: ELITEA-4723 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4723_new-unsaved-agent-instructions-open-in-edit-mode-by-default.md`).
