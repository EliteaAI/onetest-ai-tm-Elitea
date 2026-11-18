---
id: ELITEA-4730
title: "Full Screen in Edit mode preserves the Instructions draft on enter and exit (agents and skills)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4730: Full Screen in Edit mode preserves the Instructions draft on enter and exit (agents and skills)

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that Full Screen is available in Edit mode, that edits made in full screen are carried back to the inline editor, and that no data is lost or saved automatically.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" and skill "qa-7377-skill" exist, with no pending changes.

---

## Test Data

| Field | Value |
|-------|-------|
| Entities | Agent "QA-7377 Agent"; skill "qa-7377-skill" |
| Inline line | `INLINE-7377` |
| Full-screen line | `FULLSCREEN-7377` |
| Close methods | X button; Esc key; click outside the dialog (if supported) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Agent", switch INSTRUCTIONS to Edit, and add `INLINE-7377` | Save is enabled |
| 2 | Click Full Screen | The full-screen dialog opens with the current content, including `INLINE-7377` |
| 3 | In full screen, add `FULLSCREEN-7377` and close the dialog with the X button | The inline editor shows both lines. Save is enabled. Nothing has been saved yet |
| 4 | Open full screen again, make a small edit, and close with Esc. Repeat and close by clicking outside the dialog (if supported) | With each close method, the inline editor keeps all edits |
| 5 | Open full screen and click Copy to clipboard, then paste into an external editor | The pasted text is the current content, including both probe lines |
| 6 | In full screen, change "Content type" from Markdown to Text, then back to Markdown | The content is not changed or lost. Write down whether the Content type selection affects what is saved |
| 7 | Close full screen | The section is still in Edit mode |
| 8 | Click Save and reload the page | Both `INLINE-7377` and `FULLSCREEN-7377` are kept |
| 9 | Repeat steps 1–8 for "qa-7377-skill" | The results are the same as for the agent |

---

## Expected Final State

Both entities contain `INLINE-7377` and `FULLSCREEN-7377` after the explicit Save. Remove the probe lines after the run.

---

## Pass/Fail Criteria

**Pass:**
- Full-screen edits are carried back to the inline editor with every close method.
- Nothing is saved until Save is clicked, and the editor stays in Edit after full screen closes.

**Fail:**
- Edits are lost when full screen opens or closes, or are saved automatically.
- The Content type change alters the content, or the mode resets after full screen closes.

---

## Notes

- Re-run ELITEA-0059 (character counter in full screen for Welcome Message / Conversation Starter). These fields share the full-screen component, are outside the issue scope, and must not change.
