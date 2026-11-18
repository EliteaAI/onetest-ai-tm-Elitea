---
id: ELITEA-4731
title: "Instructions Preview shows no editor action icons, and Collapse field is removed in both modes"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4731: Instructions Preview shows no editor action icons, and Collapse field is removed in both modes

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify the simplified Instructions controls. Preview has only the Preview / Edit switch. Edit has only Copy to clipboard and Full Screen. Collapse field / Expand field is gone from Instructions. Other sections on the page are not affected.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agent "QA-7377 Agent" and skill "qa-7377-skill" exist. The agent has a Welcome Message and Conversation Starters.

---

## Test Data

| Field | Value |
|-------|-------|
| Entities | Agent "QA-7377 Agent"; skill "qa-7377-skill" |
| Other accordions (agent) | GENERAL, WELCOME MESSAGE, TOOLS, MODULES, SKILLS, RUN SETTINGS |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Agent" in Preview. Hover over the Instructions content and the section header | Only the Preview / Edit switch is shown. No Copy to clipboard, Full screen view or Collapse field icon appears |
| 2 | Switch to Edit and hover over the editor | Only Copy to clipboard and Full Screen are shown, each with a tooltip and an accessible label. There is no Collapse field / Expand field control |
| 3 | Click the INSTRUCTIONS accordion chevron in Preview, then in Edit | The whole section collapses and expands in both modes |
| 4 | Collapse and expand the GENERAL, WELCOME MESSAGE, TOOLS, MODULES, SKILLS and RUN SETTINGS accordions | Each accordion works as before |
| 5 | Hover over the Welcome Message and Conversation Starters fields | Their Copy / Full screen / Collapse field icons are the same as before (they are outside the issue scope). Write down what is seen |
| 6 | Repeat steps 1–3 for "qa-7377-skill" | The skill has the same control set as the agent in both modes |

---

## Expected Final State

No data is changed. Agents and skills show the same Instructions controls.

---

## Pass/Fail Criteria

**Pass:**
- Preview shows no editor action icons.
- Edit shows only Copy and Full Screen.
- Collapse field is gone from Instructions, and the other sections are unchanged.

**Fail:**
- Action icons appear in Preview, Collapse field is still present, or the agent and skill controls differ.
- Another section's controls are changed or broken.

---

## Notes

- Before the change, the agent showed Copy, Full screen and Collapse field on hover.
