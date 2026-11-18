---
id: ELITEA-4742
title: "Switching Preview and Edit preserves unsaved agent changes without auto-saving"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4742: Switching Preview and Edit preserves unsaved agent changes without auto-saving

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Verify that switching between Preview and Edit keeps the current draft, that Preview shows unsaved edits, and that switching modes never saves automatically.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" is open, with no pending changes (Save and Discard are disabled).

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent | QA-7377 Agent |
| Appended text | `## Added section QA7377` (new line) `- new bullet item` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In INSTRUCTIONS, switch to Edit | The raw Markdown source is shown in the editor |
| 2 | Append the test text at the end of the Instructions | The text is added. Save and Discard become enabled |
| 3 | Switch to Preview | "Added section QA7377" is shown as a heading and "new bullet item" as a list item. Save and Discard are still enabled |
| 4 | Switch back to Edit | The raw Markdown matches exactly what was typed, with no added or lost characters |
| 5 | Switch Preview ↔ Edit 5 times quickly | The content is unchanged and nothing is duplicated. No errors appear |
| 6 | Without saving, reload the page or open the VERSION dropdown | The unsaved-changes warning appears (or the edit is lost, if that is the existing behavior) |
| 7 | Leave without saving, then open the agent again | The stored Instructions do NOT contain "QA7377", which shows that switching modes did not save |
| 8 | Make the same edit again and click Save | Save completes. Save and Discard become disabled |
| 9 | Reload the page; check Preview, then Edit | The change is shown in both modes |

---

## Expected Final State

"QA-7377 Agent" contains the appended section only after the explicit Save in step 8.

---

## Pass/Fail Criteria

**Pass:**
- Mode switches keep the draft exactly as typed.
- Preview shows unsaved edits.
- No save happens without clicking Save.

**Fail:**
- Content is lost, duplicated or changed when modes are switched.
- Switching modes saves the agent, or turns off the unsaved-changes state.

---

## Notes

- Clean-up: remove the appended section after the run, or restore the agent from its seed content.
- Manual source: ELITEA-4724 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4724_switching-preview-and-edit-preserves-unsaved-agent-changes.md`).
