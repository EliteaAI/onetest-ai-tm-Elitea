---
id: ELITEA-0097
title: "Show Variables Toggle Appears Immediately After Adding Agent with Variables to a Pipeline (Without Page Refresh)"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3939]
---
# ELITEA-0097: Show Variables Toggle Appears Immediately After Adding Agent with Variables to a Pipeline (Without Page Refresh)

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the "Show variables" toggle label is immediately rendered on the agent's Tool Card in the Pipeline Toolkits section after an agent with `{{variable}}` placeholders is added — without requiring a manual page refresh.

**Coverage:**
- "Show variables (N)" toggle appears on the agent card immediately after the agent is added via the "+Agent" button, with no page refresh
- Toggle variable count `(N)` matches the number of `{{variable}}` placeholders defined in the agent's Instructions
- Toggle is absent before agent add and only appears for the correct card
- After a page refresh, the toggle is still present (confirms fix also holds on reload)

## Preconditions

- User is logged into elitea in the Private project
- An agent named "VarAgent" exists with at least one {{variable}} placeholder in its Instructions field (e.g., `Multiply {{a}} and {{b}}, add {{c}} and concatenate {{d}}`)
- At least one pipeline exists (or user can create one during the test)
- No page refresh has been performed since opening the pipeline configuration

## Test Data

- Agent name: VarAgent
- Instructions with variables: Multiply {{a}} and {{b}}, add {{c}} and concatenate {{d}}
- Variable count: 4 (a, b, c, d)
- Pipeline name: any existing pipeline or a newly created one (e.g., ShowVarsTestPipeline)
- Environment: {{base_url}}
- Project context: Private

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Private project → Agents sidebar. Create (or confirm existence of) an agent named "VarAgent" with Instructions: `Multiply {{a}} and {{b}}, add {{c}} and concatenate {{d}}`. Save the agent. | Agent "VarAgent" is saved successfully with 4 variable placeholders (a, b, c, d) defined in its Instructions. |
| 2 | Navigate to Pipelines from the sidebar. Open an existing pipeline in Configuration mode, or create a new one (click "Create", enter name "ShowVarsTestPipeline", save). Ensure the Toolkits section is visible. | Pipeline Configuration view is open and the Toolkits section is displayed. |
| 3 | In the Toolkits section, click the "+Agent" button. | An agent picker dropdown or modal appears, listing available agents. |
| 4 | Select "VarAgent" from the agent picker. | VarAgent is added as a toolkit card in the Toolkits list. The agent card appears on the page without a page reload. |
| 5 | Without refreshing the page, observe the "VarAgent" Tool Card in the Toolkits section. Check whether the "Show variables (4)" toggle label is visible on the card. | The "Show variables (4)" toggle is visible on the VarAgent card immediately — no page refresh is required. |
| 6 | Press F5 (hard refresh) or navigate away and back to the pipeline Configuration tab. Observe the VarAgent card again in the Toolkits section. | The "Show variables (4)" toggle is still present on the VarAgent card after the page refresh. |
| 7 | Verify no other toolkit card in the Toolkits section (e.g., a plain toolkit without variables) displays a "Show variables" toggle. | Only the VarAgent card displays the "Show variables" toggle. Other toolkit cards do not show it. |

## Expected Final State

Only the VarAgent card displays the "Show variables" toggle. Other toolkit cards do not show it.

## Pass/Fail Criteria

**Pass:**
- "Show variables (4)" toggle renders on the VarAgent card immediately after the agent is added (Step 5), without any page refresh
- Toggle persists after page refresh (Step 6)
- No other toolkit cards show a spurious "Show variables" toggle (Step 7)

**Fail:**
- "Show variables" toggle is absent from the VarAgent card immediately after adding (Step 5), requiring a page refresh to appear
- Toggle does not appear even after page refresh
- "Show variables" toggle appears on plain toolkit cards that have no variables
