---
id: ELITEA-4231
title: "Verify selected model and its Project/Shared indicator persist after Save and reload"
priority: critical
type: regression
module: llm-selector
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#7057]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is Editor in Team Project A
- Team Project A has at least one project-level LLM and access to Shared models
- Team Project A contains an agent, a pipeline and a skill

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Project | Team Project A |

Combinations (run all steps once per row):

| Entity | Where to select the model | Model | Expected indicator |
|--------|---------------------------|-------|--------------------|
| Agent | Agents → open agent → chat panel model button | project-level (e.g. `client`) | Project |
| Agent | Agents → open agent → chat panel model button | Shared (e.g. `GPT-5.6-Luna`) | Shared |
| Pipeline | Pipelines → open pipeline → Test Pipeline → chat panel model button | project-level | Project |
| Pipeline | Pipelines → open pipeline → Test Pipeline → chat panel model button | Shared | Shared |
| Skill | Skills → open skill → model selector | project-level | Project |
| Skill | Skills → open skill → model selector | Shared | Shared |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Project A, open the entity from the Test Data row | The entity editor opens |
| 2 | Open the model selector and select the model from the Test Data row | The button label shows the selected model with the expected indicator |
| 3 | Click Save | The entity is saved with no error |
| 4 | Reload the page | The entity editor reloads |
| 5 | Check the model button | The button shows the same model with the expected indicator |
| 6 | Open the model dropdown | The same entry is checked/highlighted as selected and shows the expected indicator |
| 7 | Repeat steps 1–6 for every remaining row in the Test Data table | Results match steps 1–6 for every row |

## Expected Final State

Agent, pipeline and skill each retain the selected project-level or Shared model after Save and reload, with the matching Project/Shared indicator on the button and in the dropdown.

## Pass/Fail Criteria

**Pass:**
- After reload, the button shows the saved model with the correct indicator for every row
- The same entry is marked as selected in the dropdown

**Fail:**
- The model reverts to a default or different model after reload
- The indicator after reload differs from the model's source (e.g. Shared shown as Project)
- The dropdown marks a different entry as selected, or none
