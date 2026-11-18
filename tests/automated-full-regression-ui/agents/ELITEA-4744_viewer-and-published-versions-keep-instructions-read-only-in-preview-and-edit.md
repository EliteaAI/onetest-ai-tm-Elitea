---
id: ELITEA-4744
title: "Viewer role and published versions keep Instructions read-only in Preview and Edit"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4744: Viewer role and published versions keep Instructions read-only in Preview and Edit

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the new Edit mode cannot be used to change Instructions in two cases: a Viewer opening an agent, and anyone opening a published skill version.

---

## Preconditions

- A Viewer user (User B) exists in a shared project that contains the test agent. User A has the Admin or Editor role in the same shared project.
- The test agent is created in the shared project by User A: if agent "Regression Instructions Agent" doesn't exist there, User A creates it in the shared project with the Name, Description and Instructions from Test Data and clicks Save.
- A published version of skill "regression-published-skill" exists in the shared project: if it doesn't, User A creates the skill in the shared project with the Name, Description and Instructions body from Test Data, clicks Save, and publishes that version (publishing needs moderation approval).
- An external text editor (for example, Notepad) is open.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent | Regression Instructions Agent (description: Regression agent for Instructions editor checks) |
| Agent Instructions | `# Regression heading` (new line) `Base agent instructions.` |
| Skill (published) | regression-published-skill (description: Regression skill with a published version) |
| Skill Instructions body | `# Skill regression heading` (new line) `Published skill instructions.` |
| Typing probe | `READONLY-MARKER` |

---

## Steps

### Part A: Viewer on an agent (User B)

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User B and open "Regression Instructions Agent" | The INSTRUCTIONS section renders correctly in Preview |
| 2 | If an Edit switch is offered, switch to Edit and try to type `READONLY-MARKER`, paste text, and delete text | Either no Edit switch is offered, or the editor is read-only. The content does not change |
| 3 | Check the page actions | Save, Save As Version and Discard are hidden or disabled |
| 4 | Click Copy to clipboard (in Edit mode, if the switch is offered) and paste into the external text editor | Copy to clipboard is available. The pasted text matches the agent's Instructions |
| 5 | Open Full Screen (if available) and try to type `READONLY-MARKER` | Full Screen opens read-only. No edit is possible |

### Part B: Published skill version (User A)

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | Log in as User A, open "regression-published-skill" and select its published version | The INSTRUCTIONS section renders the body in Preview. The frontmatter block is not shown |
| 7 | If an Edit switch is offered, switch to Edit and try to type `READONLY-MARKER` | Either no Edit switch is offered, or the editor is read-only. The content does not change |
| 8 | Open Full Screen (if available) and try to type `READONLY-MARKER` | Full Screen opens read-only. No edit is possible |
| 9 | Check the page actions for the published version | Save, Save As Version and Discard are hidden or disabled |

---

## Expected Final State

Neither the agent nor the published skill version is changed.

---

## Pass/Fail Criteria

**Pass:**
- In both parts, Instructions cannot be changed through inline Edit or Full Screen, and save actions are not available.
- The Viewer can copy the agent Instructions.

**Fail:**
- Any text can be changed, or Save / Save As Version / Discard becomes available.
- Copy to clipboard is missing for the Viewer, or the pasted text does not match.

---

## Notes

- The published agent version is covered by ELITEA-2614 (step 10 updated in this PR). The Viewer on a skill is covered by ELITEA-4748.
- Also re-run the existing cases (not duplicated here): ELITEA-4374 (Viewer: save actions hidden), ELITEA-4373 (backend rejects Viewer saves), ELITEA-4379 (Viewer version dropdown), ELITEA-3328 (compare versions respects permissions), ELITEA-4376 (Viewer on skill details).
- Manual source: ELITEA-4734 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4734_viewer-and-published-versions-keep-instructions-read-only-in-preview-and-edit.md`).
