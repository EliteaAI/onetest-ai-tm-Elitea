---
id: ELITEA-0832
title: "Nested Agent and Pipeline Chipsets Display Correct Names at All Levels"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0832: Nested Agent and Pipeline Chipsets Display Correct Names at All Levels

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
- "Main Pipeline" exists and contains a step calling "Sub Pipeline"
- "Sub Pipeline" exists and contains a step calling "Leaf Agent"
- "Leaf Agent" exists and is functional
- Browser: Chrome/Edge latest

## Test Data

- Main Pipeline: contains a step calling Sub Pipeline
- Sub Pipeline: contains a step calling Leaf Agent
- Leaf Agent: any functional agent
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Navigate to Pipelines in the left sidebar. Confirm the following hierarchy exists: Main Pipeline → (step calling) Sub Pipeline → (step calling) Leaf Agent. Open Main Pipeline. | Main Pipeline detail page loads; nested structure is confirmed in configuration. |
| 2 | Click Run on Main Pipeline. Wait for the full execution to complete (all three levels must finish). | Main Pipeline executes; nested execution fan-out is triggered. |
| 3 | Navigate to Main Pipeline's History Runs tab. Open the most recent completed run to view the execution trace. | Execution trace for the run is displayed. |
| 4 | At the top level of the execution trace, locate the first chipset entry. Read its label and identify its icon type. | Chipset label reads 'Main Pipeline' with a Pipeline icon (not an Agent icon or generic icon). |
| 5 | Expand or drill into the execution to show the second level (the step where Sub Pipeline was called). Locate the chipset for this nested element. Read its label and icon type. | Chipset label reads 'Sub Pipeline' with a Pipeline icon — NOT 'Main Pipeline', NOT 'unnamed', NOT a blank/generic label. |
| 6 | Expand or drill further into Sub Pipeline's execution to reveal the third level (the step where Leaf Agent was called). Locate the chipset for this element. Read its label and icon type. | Chipset label reads 'Leaf Agent' with an Agent icon (not a Pipeline icon) — NOT 'Sub Pipeline' or 'Main Pipeline'. |
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
