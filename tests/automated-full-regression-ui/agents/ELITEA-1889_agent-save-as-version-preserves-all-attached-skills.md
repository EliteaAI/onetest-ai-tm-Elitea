---
id: ELITEA-1889
title: "Agent \"Save As Version\" preserves all attached Skills"
priority: critical
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_save_as_version_preserves_skills.TestAgentSaveAsVersionPreservesSkills.test_agent_save_as_version_preserves_skills
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/558
---

# ELITEA-1889: Agent "Save As Version" preserves all attached Skills

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that saving an agent as a new version preserves all attached Skills in the new version.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Skill named "VersionedSkill" is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Attached skill | VersionedSkill |
| Version name | v1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create an Agent with at least one attached Skill ("VersionedSkill") | The agent is created with "VersionedSkill" listed in the SKILLS section |
| 2 | Click "Save As Version" → enter name "v1" → confirm | The version "v1" is created successfully |
| 3 | Open version "v1" in the Agent editor | The "v1" version is loaded in the agent editor |
| 4 | Verify "VersionedSkill" is still listed in the SKILLS section | "VersionedSkill" is present in the SKILLS section of version "v1" |

---

## Expected Final State

Version "v1" of the agent retains "VersionedSkill" in its SKILLS section, confirming skill attachments are preserved during versioning.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- "VersionedSkill" is listed in the SKILLS section of the newly created version "v1".

**Fail:**
- Any step produces an error or unexpected result.
- "VersionedSkill" is missing from the SKILLS section of version "v1".
