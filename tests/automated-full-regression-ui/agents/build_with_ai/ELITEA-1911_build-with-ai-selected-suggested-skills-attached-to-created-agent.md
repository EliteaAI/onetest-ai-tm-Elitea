---
id: ELITEA-1911
title: "Build with AI — selected suggested Skills are attached to the created agent"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAISelectedResourcesAttached.test_selected_suggested_skill_attached_and_non_selected_absent
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/599
---

# ELITEA-1911: Build with AI — selected suggested Skills are attached to the created agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that Skills explicitly selected in the Suggested Skills section are attached to the created agent, while non-selected skills are absent from the SKILLS section.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The generated draft includes a visible "SUGGESTED SKILLS" section with at least two skill cards.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft with a Suggested Skills section visible | The review form is displayed with the SUGGESTED SKILLS section containing skill cards |
| 2 | Select one or more suggested Skills by clicking their cards | The selected Skill cards become highlighted/selected |
| 3 | Click "Approve" / "Create Agent" | The agent creation is initiated |
| 4 | Open the created Agent | The Agent detail page is displayed |
| 5 | Verify the selected Skills appear in the SKILLS section of the Agent | The explicitly selected Skills are present in the SKILLS section |
| 6 | Verify non-selected suggested Skills are absent from the SKILLS section | Skills that were not selected do not appear in the SKILLS section |

---

## Expected Final State

The created agent's SKILLS section contains only the explicitly selected skills; non-selected suggested skills are not attached.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Selected Skills are attached; non-selected Skills are absent from the SKILLS section.

**Fail:**
- Any step produces an error or unexpected result.
- A selected Skill is not attached, or a non-selected Skill is incorrectly attached.
