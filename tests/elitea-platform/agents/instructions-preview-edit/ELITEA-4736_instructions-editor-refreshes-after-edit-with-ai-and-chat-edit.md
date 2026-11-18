---
id: ELITEA-4736
title: "Instructions editor shows changes made by Edit with AI and chat edit in Preview and Edit"
priority: high
type: integration
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4736: Instructions editor shows changes made by Edit with AI and chat edit in Preview and Edit

**Module:** agents · **Priority:** high · **Type:** integration

**Objective:** Verify that changes to agent Instructions made outside the inline editor (Edit with AI, and chat-driven edits through the MCP safe-patch tool) are shown correctly in the new Preview and Edit modes, and that Save / Discard still behave correctly.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" is saved (not published), with no pending changes.
- Chat-based agent editing (internal MCP tools) is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | QA-7377 Agent |
| Edit with AI request | `Add a final section "## Closing" with one sentence: Thank you for using QA-7377.` |
| Chat edit request | `In agent QA-7377 Agent, add the line "CHAT-EDIT-7377" to the end of the instructions.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Agent" in Preview. Run Edit with AI with the test request and apply the result | The Instructions update without a page reload. Preview shows the "Closing" heading |
| 2 | Switch to Edit | The raw source contains the new section exactly as Preview shows it |
| 3 | Check Save and Discard | They are enabled if the change was applied as an unsaved draft (or the change is already stored, per the existing behavior). Write down which one applies |
| 4 | Click Discard (if enabled) and confirm | The Instructions return to the saved value in both modes |
| 5 | Open a conversation and send the chat edit request. Approve the tool call if asked | The chat reports a successful patch |
| 6 | Open "QA-7377 Agent" (or reload the page) | Preview shows `CHAT-EDIT-7377`. Edit shows the same line in the source |

---

## Expected Final State

"QA-7377 Agent" contains `CHAT-EDIT-7377`. Remove it after the run.

---

## Pass/Fail Criteria

**Pass:**
- Changes from Edit with AI and from chat edits are shown correctly in both modes, and Save / Discard behave as before.

**Fail:**
- Preview or Edit shows stale content, or the two modes show different content.
- Discard does not revert a change made by Edit with AI.

---

## Notes

- Also re-run the existing cases (not duplicated here): Compare Versions for agents (ELITEA-3319, ELITEA-3321, ELITEA-3351) and for skills (ELITEA-3334, ELITEA-3336, ELITEA-3352); Edit with AI (ELITEA-2611 for skills, ELITEA-2759 for published agents); chat edit (ELITEA-3097, ELITEA-3102).
