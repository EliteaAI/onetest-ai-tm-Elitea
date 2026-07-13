---
id: ELITEA-1909
title: "Build with AI — selected suggested resources are attached to the created agent"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1909: Build with AI — selected suggested resources are attached to the created agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that only explicitly selected suggested resources (Toolkit, nested Agent) are attached to the created agent, and non-selected resources are absent.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- A GitHub toolkit exists in the project.
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit to select | GitHub toolkit (pre-existing) |

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
