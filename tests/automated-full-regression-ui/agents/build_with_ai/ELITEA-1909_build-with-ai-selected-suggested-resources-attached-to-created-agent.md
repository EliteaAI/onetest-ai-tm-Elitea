---
id: ELITEA-1909
title: "Build with AI — selected suggested resources are attached to the created agent"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAISelectedResourcesAttached.test_selected_suggested_resources_attached_and_non_selected_absent
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/573
---

# ELITEA-1909: Build with AI — selected suggested resources are attached to the created agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that only explicitly selected suggested resources (Toolkit, nested Agent) are attached to the created agent, and non-selected resources are absent.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- A GitHub toolkit exists in the project.
- **An Agent relevant to the generation prompt (e.g., GitHub/Jira-related) exists in the project.** The "Build with AI" suggestion engine populates the "Suggested Agents:" section only when the project has Agents whose name/description are semantically relevant to the submitted prompt. With zero relevant Agents in inventory, the suggested agents array is empty and steps 4 and 8 cannot be executed. Create at least one Agent with a GitHub-related name and description before starting this test. (Clarification per elitea-testing-public#572)
- The GenerateAgentModal is accessible from the New Agent creation page.

**Note on Agent Suggestion**: The "Suggested Agents:" section appears only when the project contains Agents semantically relevant to the generation prompt. If no relevant Agent exists, the section will not render, and steps 4 and 8 cannot be executed. This is expected platform behavior, not a defect.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit to select | GitHub toolkit (pre-existing) |
| Fixture Agent (for suggestion) | At least one Agent with GitHub-related name/description (e.g., "GitHub Issue Bot", "GitHub PR Reviewer") to populate the "Suggested Agents:" section |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Github toolkit | The GitHub toolkit is created and available in the project |
| 2 | Generate an agent draft that mentions this toolkit | The review form is displayed with the GitHub toolkit listed in Suggested Resources |
| 3 | In the review form, select the suggested Toolkit by clicking it | The Toolkit card is highlighted/selected |
| 4 | Select the suggested Agent by clicking it | The Agent card is highlighted/selected |
| 5 | Click "Approve" / "Create Agent" | The agent creation is initiated |
| 6 | Open the created Agent | The Agent detail page is displayed |
| 7 | Verify the selected Toolkit is present in the TOOLKITS section | The GitHub toolkit appears in the TOOLKITS section of the created agent |
| 8 | Verify the selected nested Agent is present in the TOOLKITS section | The selected nested Agent appears in the appropriate section |
| 9 | Verify any resources that were NOT selected are absent | Non-selected suggested resources are not attached to the agent |

---

## Expected Final State

The created agent has the explicitly selected Toolkit and nested Agent attached, while any non-selected suggested resources are absent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Selected resources appear in the agent; non-selected resources are absent.

**Fail:**
- Any step produces an error or unexpected result.
- A selected resource is not attached, or a non-selected resource is incorrectly attached.
