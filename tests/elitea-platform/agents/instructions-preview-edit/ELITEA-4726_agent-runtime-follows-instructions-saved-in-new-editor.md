---
id: ELITEA-4726
title: "Agent runtime follows Instructions saved in the new editor (agent chat, conversation, pipeline)"
priority: critical
type: integration
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4726: Agent runtime follows Instructions saved in the new editor (agent chat, conversation, pipeline)

**Module:** agents · **Priority:** critical · **Type:** integration

**Objective:** Verify that, after the editor change, the agent still runs with the saved Instructions in every runtime context.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Agent "QA-7377 Agent" Instructions include the rule `Always start your answer with the word PINEAPPLE.` The agent has been saved at least once using the new Edit mode.
- Pipeline "QA-7377 Pipeline" has an Agent node that calls "QA-7377 Agent".

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent | QA-7377 Agent |
| Pipeline | QA-7377 Pipeline |
| Prompt | `Hello` |
| Expected marker | Answer starts with `PINEAPPLE` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Agent". In Preview, check that the PINEAPPLE rule is shown | The rule is shown in the rendered Instructions |
| 2 | In the agent's built-in chat panel, send `Hello` | The answer starts with "PINEAPPLE" |
| 3 | Start a new conversation in Chat, add "QA-7377 Agent" as a participant, and send `Hello` | The answer starts with "PINEAPPLE" |
| 4 | Open "QA-7377 Pipeline" and run it with input `Hello` | The Agent node output starts with "PINEAPPLE". The pipeline finishes without errors |
| 5 | In the agent, switch to Edit, change the rule to `Always start your answer with the word MANGO.`, and click Save | Save succeeds |
| 6 | Repeat step 3 in a new conversation | The answer starts with "MANGO", which shows that the latest saved Instructions are used |

---

## Expected Final State

The agent and the pipeline use the latest saved Instructions. Restore the PINEAPPLE rule after the run.

---

## Pass/Fail Criteria

**Pass:**
- In all three contexts (agent chat, conversation, pipeline), the response follows the saved Instructions.

**Fail:**
- Instructions are ignored, out of date, or break execution in any context.

---

## Notes

- Re-run ELITEA-1897 (agent executes with name/description only).
- Frontmatter exclusion at runtime (if implemented) is covered by ELITEA-4727.
