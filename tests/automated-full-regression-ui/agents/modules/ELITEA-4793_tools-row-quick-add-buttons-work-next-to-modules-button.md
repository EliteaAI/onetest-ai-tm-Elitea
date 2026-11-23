---
id: ELITEA-4793
title: "+ Toolkit, + MCP, + Agent and + Pipeline buttons still work in the Tools row next to the + Modules button"
priority: critical
type: regression
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents, nfr:ui, modules, regression, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4793: + Toolkit, + MCP, + Agent and + Pipeline buttons still work in the Tools row next to the + Modules button

**Module:** Agents · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that the existing quick-add buttons in the Agent TOOLS row still open their flows after "+ Modules" was added, including when the Modules dropdown is open, and that adding a tool does not change module states.

## Preconditions

- Logged in to `{{base_url}}`
- An editable Agent exists
- At least one toolkit exists in the project
- Browser: Chrome (latest)

## Test Data

| Field | Value |
|---|---|
| Toolkit | Any existing toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent and click "+ Toolkit", then dismiss | Toolkit dialog opens and closes |
| 2 | Click "+ MCP", then dismiss | MCP dialog opens and closes |
| 3 | Click "+ Agent", then dismiss | Agent dialog opens and closes |
| 4 | Click "+ Pipeline", then dismiss | Pipeline dialog opens and closes |
| 5 | Click "+ Modules" and note module states, then click "+ Toolkit" | Modules dropdown closes and the Toolkit dialog opens |
| 6 | Add the existing toolkit and click Save | Toolkit card appears in TOOLS; Agent is saved |
| 7 | Click "+ Modules" | Module states are the same as noted in step 5 |
| 8 | Cleanup: remove the toolkit and click Save | Toolkit card is removed |

## Expected Final State

All quick-add buttons work and module states are unaffected by adding tools.

## Pass/Fail Criteria

**Pass:**
- Every quick-add button opens the correct flow, including from an open Modules dropdown; module states unchanged

**Fail:**
- Any button is broken or blocked by the dropdown, or adding a tool changes module states

## Notes

**Source functional tests:** ELITEA-4787 (related: ELITEA-0046)
**Regression rationale:** + Modules shares the TOOLS row and menu component with the other quick-add buttons; protects against side effects on adding tools.
**Selected checkpoints:** Each button opens its dialog; works from open dropdown; module states unchanged after adding a toolkit.
