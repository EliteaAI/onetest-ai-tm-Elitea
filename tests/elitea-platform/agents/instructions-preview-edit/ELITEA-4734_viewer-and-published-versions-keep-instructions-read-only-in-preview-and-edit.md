---
id: ELITEA-4734
title: "Viewer role and published versions keep Instructions read-only in Preview and Edit"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4734: Viewer role and published versions keep Instructions read-only in Preview and Edit

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the new Edit mode cannot be used to change Instructions as a Viewer or on a published version.

---

## Preconditions

- User A has the Admin or Editor role. User B has the Viewer role in a shared project.
- The shared project contains copies of "QA-7377 Agent" and "qa-7377-skill".
- Agent "QA-7377 Published" has a published version (publish it first if needed; this needs approval).
- A skill with a published version is available.

---

## Test Data

| User / version | Entity |
|---|---|
| User B (Viewer) | Shared-project agent "QA-7377 Agent" |
| User B (Viewer) | Shared-project skill "qa-7377-skill" |
| User A | Published version of "QA-7377 Published" |
| User A | Published skill version |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the user in the first row of the Test Data table and open the entity | The INSTRUCTIONS section renders correctly in Preview |
| 2 | If an Edit switch is available, switch to Edit and try to type, paste or delete text | The editor is read-only. The content does not change |
| 3 | Check the page actions | Save, Save As Version and Discard are hidden or disabled |
| 4 | Click Copy to clipboard and paste into an external editor | Copy works for reading (or the agreed design applies). The pasted text matches the content |
| 5 | Open Full Screen and try to type | Full screen opens read-only. No edit is possible |
| 6 | Repeat steps 1–5 for every other row in the Test Data table | Every combination stays read-only |

---

## Expected Final State

None of the entities are changed.

---

## Pass/Fail Criteria

**Pass:**
- In every combination, Instructions cannot be changed through inline Edit or Full Screen, and save actions are not available.

**Fail:**
- Any text can be changed, or Save / Save As Version / Discard becomes available.

---

## Notes

- Also re-run the existing cases (not duplicated here): ELITEA-4374 (Viewer: save actions hidden), ELITEA-4373 (backend rejects Viewer saves), ELITEA-4379 (Viewer version dropdown), ELITEA-3328 (compare versions respects permissions), ELITEA-2614 (published version cannot be modified), ELITEA-4376 (Viewer on skill details).
