---
id: ELITEA-4230
title: "Verify LLM selector opens, lists all models with Project/Shared indicator and selects a model in every product area"
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
- Team Project A has at least 2 project-level LLM configurations (e.g. `client`) and also has access to Shared models (e.g. `Bedrock-GPT-5.6-Luna`, `GPT-5.6-Luna`, `Anthropic Claude 5 Sonnet`)
- Team Project A contains an agent (e.g. `AB_test`), a published agent, a pipeline with an LLM node and a skill
- DevTools Console is open

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Project | Team Project A |
| Project-level model | `client` |
| Shared model | `GPT-5.6-Luna` |
| Message | `Hello` |

Locations (run all steps once per row):

| Location | How to open the LLM selector |
|----------|------------------------------|
| Chat | Chats → open or create a conversation → bottom bar model button ("Select LLM Model") |
| Agent editor | Agents → open an agent → chat panel model button |
| Published agent in Chat | Add a published agent to a chat → model button |
| Pipeline | Pipelines → open a pipeline → Test Pipeline → chat panel model button |
| Skill | Skills → open a skill → model selector |
| Chat canvas | Open a pipeline or agent from the Chat canvas → model dropdown |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → AI Configuration in Project A and note the project-level LLMs; note the available Shared models | Reference list of expected models is recorded |
| 2 | Navigate to the location from the Test Data table and click the LLM model button | The dropdown opens; the list is not blank; no errors appear in the console |
| 3 | Count the entries in the dropdown and compare them with the reference list from step 1 | The number and names of entries match the project-level plus Shared models |
| 4 | Inspect each entry in the dropdown | Every entry shows an indicator: Project icon for project-level models, Shared icon for Shared models |
| 5 | Select the project-level model `client` | Dropdown closes; the button label changes to `client` |
| 6 | Send the message `Hello` | A response is returned by the selected model |
| 7 | Open the dropdown again and select the Shared model `GPT-5.6-Luna` | Dropdown closes; the button label changes to `GPT-5.6-Luna` |
| 8 | Send the message `Hello` | A response is returned by the selected model |
| 9 | Repeat steps 2–8 for every remaining location in the Test Data table | Results match steps 2–8 in every location |

## Expected Final State

In all six locations the LLM selector opens, lists every project-level and Shared model with the correct Project/Shared indicator, and both a project-level and a Shared model can be selected and used to get a response.

## Pass/Fail Criteria

**Pass:**
- The dropdown opens with a complete list and no console errors in every location
- Every entry shows the correct Project or Shared indicator
- Selecting a model updates the button label and the model responds to `Hello`

**Fail:**
- The dropdown is blank, fails to open, or logs console errors in any location
- Any model is missing, duplicated, or has no indicator or the wrong indicator
- Selection does not update the button label, or no response is returned
