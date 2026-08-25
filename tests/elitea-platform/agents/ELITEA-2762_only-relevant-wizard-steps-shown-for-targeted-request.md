---
id: ELITEA-2762
title: "Only relevant wizard steps are displayed when user specifies particular fields"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent with all fields configured is open

## Test Data

| Prompt | Expected Wizard Steps |
|--------|----------------------|
| "Improve only the agent name and description" | General, Summary |
| "Update the instructions" | Instructions, Summary |
| "Add a better welcome message and conversation starters" | User Interaction, Summary |
| "Suggest relevant tools and skills" | Tools & Skills, Summary |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent's configuration page and click "Edit with AI" | Modal opens |
| 2 | Enter prompt "Improve only the agent name and description" and generate | Wizard shows only General and Summary steps |
| 3 | Cancel and re-open Edit with AI, enter prompt "Update the instructions" and generate | Wizard shows only Instructions and Summary steps |
| 4 | Cancel and re-open Edit with AI, enter prompt "Add a better welcome message and conversation starters" and generate | Wizard shows only User Interaction and Summary steps |
| 5 | Cancel and re-open Edit with AI, enter prompt "Suggest relevant tools and skills" and generate | Wizard shows only Tools & Skills and Summary steps |
| 6 | For each of steps 2–5, confirm Summary is always the final step shown | Summary appears last in every case |

## Expected Final State

For each targeted prompt, only the steps containing the relevant fields are shown, with Summary always present as the final step.

## Pass/Fail Criteria

**Pass:**
- Wizard step sets match the table above for each of the 4 targeted prompts, with Summary always last

**Fail:**
- An irrelevant step is shown, a relevant step is missing, or Summary is absent/misplaced
