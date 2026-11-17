---
id: ELITEA-0832
title: "Nested Agent and Pipeline Chipsets Display Correct Names at All Levels"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1, epic:7093]
requirements: [ProjectAlita/projectalita.github.io#3535, EliteaAI/elitea_issues#3734]
---
# ELITEA-0832: Nested Agent and Pipeline Chipsets Display Correct Names at All Levels

> **Updated for Pipelines 2.0:** UI wording only. Nested levels are inspected in the chat thinking steps. The Run Details timeline groups a nested agent/pipeline call into one step and does not expand it (#3734).

> Retest pending

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that in multi-level nested execution (Pipeline → Pipeline → Agent), each entity's chipset shows its own name correctly at every nesting level.

**Coverage:**
- Top-level chipset shows "Main Pipeline" with a Pipeline icon
- Second-level nested chipset shows "Sub Pipeline" with a Pipeline icon (not parent name)
- Third-level nested chipset shows "Leaf Agent" with an Agent icon (not Pipeline icon)
- No nesting level inherits or duplicates a parent's name
- No generic or blank labels at any nesting level

## Preconditions

- Logged in to ELITEA at {{base_url}}
- "Main Pipeline" exists and contains an Agent node calling "Sub Pipeline"
- "Sub Pipeline" exists and contains an Agent node calling "Leaf Agent"
- "Leaf Agent" exists and is functional
- Browser: Chrome/Edge latest

## Test Data

- Main Pipeline: contains an Agent node calling Sub Pipeline
- Sub Pipeline: contains an Agent node calling Leaf Agent
- Leaf Agent: any functional agent
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Navigate to Pipelines in the left sidebar. Confirm the hierarchy exists: Main Pipeline → (Agent node calling) Sub Pipeline → (Agent node calling) Leaf Agent. Open Main Pipeline. | Main Pipeline detail page loads; nested structure is confirmed in configuration. |
| 2 | Open Test Pipeline and send a message. Wait for the full execution to complete (all three levels must finish). | Main Pipeline executes; nested execution is triggered. |
| 3 | In the chat response, expand the thinking steps (or open the run from Run History) to view the execution trace. | Execution trace for the run is displayed. |
| 4 | At the top level of the execution trace, locate the first chipset entry. Read its label and identify its icon type. | Chipset label reads 'Main Pipeline' with a Pipeline icon (not an Agent icon or generic icon). |
| 5 | Expand the second level (the step where Sub Pipeline was called). Locate the chipset for this nested element. Read its label and icon type. | Chipset label reads 'Sub Pipeline' with a Pipeline icon — NOT 'Main Pipeline', NOT 'unnamed', NOT a blank/generic label. |
| 6 | Expand further into Sub Pipeline's execution to reveal the third level (the step where Leaf Agent was called). Locate the chipset for this element. Read its label and icon type. | Chipset label reads 'Leaf Agent' with an Agent icon (not a Pipeline icon) — NOT 'Sub Pipeline' or 'Main Pipeline'. |
| 7 | Review all three levels side by side on screen. Confirm that each level displays exclusively its own entity name and no level shows a parent entity's name, a generic placeholder, or a blank. | All three levels: 'Main Pipeline' (Pipeline icon), 'Sub Pipeline' (Pipeline icon), 'Leaf Agent' (Agent icon) — correct names, correct icons, no duplication. |

## Expected Final State

All three levels: 'Main Pipeline' (Pipeline icon), 'Sub Pipeline' (Pipeline icon), 'Leaf Agent' (Agent icon) — correct names, correct icons, no duplication.

## Pass/Fail Criteria

**Pass:**
- Level 1: "Main Pipeline" with Pipeline icon
- Level 2: "Sub Pipeline" with Pipeline icon (not "Main Pipeline", not blank)
- Level 3: "Leaf Agent" with Agent icon (not Pipeline icon, not parent name)
- Each level shows only its own entity name

**Fail:**
- Any level shows a parent entity's name
- Any level shows a generic label, unnamed, or blank
- Agent level shows a Pipeline icon instead of Agent icon
