---
id: ELITEA-1789
title: "Attach a Skill to an Agent and verify it appears with version selector"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_skill_agent_version_selector.TestAttachSkillToAgentWithVersionSelector.test_attach_skill_to_agent_with_version_selector
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/47
---

# ELITEA-1789: Attach a Skill to an Agent and verify it appears with version selector

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that a Skill can be attached to an Agent and that the attached Skill entry displays a version selector in the Agent configuration UI.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- At least one Skill with at least one saved version exists in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill name | (any existing Skill with at least one version, e.g. "Formatter") |
| Skill version | base (default) |
| Agent name | (any new Agent name, e.g. "Test Agent") |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents and create a new Agent (or open an existing one in edit mode) | Agent creation / edit form is open |
| 2 | Locate the Skills attachment section in the Agent configuration | Skills attachment area is visible |
| 3 | Click to add a Skill and select an existing Skill from the list | Selected Skill appears in the attached Skills list |
| 4 | Verify that the attached Skill entry displays a version selector | A version selector (dropdown or similar control) is shown next to the Skill name |
| 5 | Confirm the default selected version in the version selector | The default version is pre-selected (e.g., `base`) |
| 6 | Save the Agent | Agent saves without errors; the Skill remains attached with the selected version |

---

## Expected Final State

The Agent is saved with the Skill attached. The Skill entry in the Agent configuration includes a functional version selector showing the currently selected version.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The attached Skill entry shows a version selector with a valid default version.
- Agent saves successfully with the Skill attached.

**Fail:**
- Any step produces an error or unexpected result.
- No version selector is shown for the attached Skill.
- Agent fails to save with the Skill attached.
