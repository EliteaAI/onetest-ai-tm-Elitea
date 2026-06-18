---
id: ELITEA-0106
title: "Agent/Pipeline name is displayed in the page header"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:agents, issue:3707, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3707]
---
# ELITEA-0106: Agent/Pipeline name is displayed in the page header

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the agent/pipeline name is displayed prominently in the page header for both entity types.

**Coverage:**
- Agent/Pipeline name visible in the header next to the back arrow
- Displayed name matches the saved entity name

https://www.figma.com/design/5vWxC85QBhqbzPU30RP7LH/Alita.-Prompt-Library?node-id=22403-15384&p=f&t=dGdevYKWjPHLJti4-0

https://www.figma.com/design/5vWxC85QBhqbzPU30RP7LH/Alita.-Prompt-Library?node-id=17942-185231&p=f&t=tIQfYJFJTtAYkFIf-0

## Preconditions

- Logged in to {{base_url}} with a valid user account
- At least one Agent and one Pipeline exist in the project

## Test Data

- Agent name: e.g. `Test Agent` (any existing agent)
- Pipeline name: e.g. `Test Pipeline` (any existing pipeline)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent/Pipeline page. Open any existing agent/pipeline. | Agent/Pipeline detail page opens. |
| 2 | Observe the top header area (next to the back arrow ←). | The agent's/pipeline's name is displayed in the header. |
| 3 | Verify the displayed name matches the value in the Name field of the configuration form. | Name in the header matches the saved agent/pipeline name. |

## Expected Final State

Name in the header matches the saved agent/pipeline name.

## Pass/Fail Criteria

**Pass:**
- Agent/pipeline name is visible in the header next to the back arrow
- Displayed name matches the actual saved entity name

**Fail:**
- Header shows no name, a placeholder, or an incorrect name for either entity type
