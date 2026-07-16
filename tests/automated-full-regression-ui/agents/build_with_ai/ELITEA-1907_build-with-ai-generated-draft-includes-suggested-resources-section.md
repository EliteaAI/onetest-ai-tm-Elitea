---
id: ELITEA-1907
title: "Build with AI — generated draft includes suggested resources section"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAISuggestedResources.test_generated_draft_includes_suggested_resources_section
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/543
---

# ELITEA-1907: Build with AI — generated draft includes suggested resources section

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that when a description implying resource use is submitted, the generated draft review form includes a Suggested Resources section with relevant suggestions from Toolkits, Agents, Pipelines, and MCPs — none pre-selected.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- Toolkits, Agents, Pipelines, and/or MCPs exist in the project that could be suggested.
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "An agent that queries GitHub and runs Jira updates" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal and submit a description implying resource use: "An agent that queries GitHub and runs Jira updates" | The modal shows a loading state and then transitions to the review form |
| 2 | Wait for generation to complete | The review/edit form is displayed |
| 3 | Verify a Suggested Resources section is shown containing relevant suggestions from: Toolkits, Agents, Pipelines, MCPs | The Suggested Resources section is present and populated with relevant resource suggestions |
| 4 | Verify each suggested resource shows its name and description | Each resource card displays both a name and a description |
| 5 | Verify no resource is pre-selected or auto-linked — all require explicit user selection | All suggested resource cards appear in an unselected state |

---

## Expected Final State

The review form displays a Suggested Resources section with relevant Toolkits, Agents, Pipelines, and/or MCP suggestions, each showing name and description, and none pre-selected.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Suggested Resources section is present, contains relevant suggestions with name and description, and no resource is pre-selected.

**Fail:**
- Any step produces an error or unexpected result.
- The Suggested Resources section is absent, shows no suggestions, or any resource is auto-selected.
