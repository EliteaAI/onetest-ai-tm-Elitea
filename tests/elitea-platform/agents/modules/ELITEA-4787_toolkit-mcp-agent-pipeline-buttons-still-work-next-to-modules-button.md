---
id: ELITEA-4787
title: "+ Toolkit, + MCP, + Agent and + Pipeline buttons still work in the Tools row next to the + Modules button"
priority: critical
type: regression
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, regression, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4787: + Toolkit, + MCP, + Agent and + Pipeline buttons still work in the Tools row next to the + Modules button

**Module:** Agents · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that adding the "+ Modules" button to the TOOLS row does not break the existing quick-add buttons (+ Toolkit, + MCP, + Agent, + Pipeline) and that they work while the Modules dropdown is open.

**Coverage:**
- Each quick-add button opens the correct flow
- Interaction from an open Modules dropdown
- Adding a tool does not change module states

> Related: ELITEA-0046 (expects 4 buttons in the TOOLS row — needs update to 5 buttons after #7380).

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists
- At least one toolkit, MCP, Agent and Pipeline exist in the project
- Browser: Chrome (latest)

## Test Data

Any existing editable Agent; any existing toolkit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent and locate the TOOLS row | Buttons + Toolkit, + MCP, + Agent, + Pipeline and + Modules are displayed |
| 2 | Click "+ Toolkit", then dismiss the dialog | Toolkit selection dialog opens and closes; TOOLS row unchanged |
| 3 | Click "+ MCP", then dismiss the dialog | MCP selection dialog opens and closes |
| 4 | Click "+ Agent", then dismiss the dialog | Agent selection dialog opens and closes |
| 5 | Click "+ Pipeline", then dismiss the dialog | Pipeline selection dialog opens and closes |
| 6 | Click "+ Modules" and, with the dropdown open, click "+ Toolkit" | Modules dropdown closes and the Toolkit dialog opens |
| 7 | Add an existing toolkit to the Agent | Toolkit card appears in the TOOLS section |
| 8 | Click "+ Modules" | Module switch states are unchanged by adding the toolkit |
| 9 | Click Save and reload the page | Toolkit card and module states are kept |

## Expected Final State

All quick-add buttons work as before, and the Modules dropdown coexists with them.

## Pass/Fail Criteria

**Pass:** Every quick-add button opens the correct flow, including from an open Modules dropdown, and module states are not affected
**Fail:** Any quick-add button is missing, broken, blocked by the Modules dropdown, or adding a tool changes module states
