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

**Objective:** Verify that switching between Preview and Edit keeps the current draft, that Preview shows unsaved edits, that switching modes never saves automatically, and that the unsaved-changes warning appears both on page reload and on version switch.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "Regression Instructions Agent" exists with the Instructions from Test Data. If it doesn't exist, create it with the Name, Description and Instructions from Test Data and click Save.
- The agent has a second version named `regression-v2`. If it doesn't exist, open the agent and click Save As Version with the name `regression-v2`.
- The `base` version of "Regression Instructions Agent" is open, with no pending changes (Save and Discard are disabled).

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent name | Regression Instructions Agent |
| Agent description | Regression agent for Instructions editor checks |
| Second version | `regression-v2` |
| Appended text | `## Added section REGRESSION-MARKER` (new line) `- new bullet item` |

Agent Instructions (used only when the agent has to be created):

~~~markdown
# Regression heading
## Rules
1. First rule
2. Second rule

- Bullet item
- **Bold item** with `inline code`
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In INSTRUCTIONS, switch to Edit | The raw Markdown source is shown in the editor |
| 2 | Append the test text at the end of the Instructions | The text is added. Save and Discard become enabled |
| 3 | Switch to Preview | "Added section REGRESSION-MARKER" is shown as a heading and "new bullet item" as a list item. Save and Discard are still enabled |
| 4 | Switch back to Edit | The raw Markdown matches exactly what was typed, with no added or lost characters |
| 5 | Switch Preview ↔ Edit 5 times quickly | The content is unchanged and nothing is duplicated. No errors appear |
| 6 | Reload the page (F5) | An unsaved-changes warning appears. Choose to stay on the page: the draft with "REGRESSION-MARKER" is still in the editor |
| 7 | In the VERSION dropdown, select `regression-v2` | An unsaved-changes warning appears. Choose to stay: the `base` version is still open, and the draft with "REGRESSION-MARKER" is still in the editor |
| 8 | Select `regression-v2` again and, in the warning, choose to leave without saving. Then select `base` | `regression-v2` opens. When `base` opens again, its Instructions do NOT contain "REGRESSION-MARKER", which shows that switching modes did not save |
| 9 | Make the same edit again and click Save | Save completes. Save and Discard become disabled |
| 10 | Reload the page; check Preview, then Edit | The change is shown in both modes |

---

## Expected Final State

The `base` version of "Regression Instructions Agent" contains the appended section only after the explicit Save in step 9. Remove the appended section after the run.

---

## Pass/Fail Criteria

**Pass:**
- Mode switches keep the draft exactly as typed, and Preview shows unsaved edits.
- The unsaved-changes warning appears both on reload and on version switch.
- No save happens without clicking Save.

**Fail:**
- Content is lost, duplicated or changed when modes are switched.
- The warning is missing on reload or on version switch.
- Switching modes saves the agent, or turns off the unsaved-changes state.

---

## Notes

- Skill equivalent: ELITEA-4746.
- Clean-up: remove the appended section after the run.
- Manual source: ELITEA-4724 (`tests/elitea-platform/agents/instructions-preview-edit/ELITEA-4724_switching-preview-and-edit-preserves-unsaved-agent-changes.md`).
