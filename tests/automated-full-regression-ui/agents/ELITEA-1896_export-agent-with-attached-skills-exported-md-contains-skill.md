---
id: ELITEA-1896
title: "Export Agent with attached Skills — exported .md contains Skill content"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: automation.tests.ui.skills.test_export_agent_with_attached_skills.TestExportAgentWithAttachedSkills.test_export_agent_with_attached_skills
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/597
duplicate_of: ELITEA-1794
note: "Behavioural duplicate of ELITEA-1794 (same objective/steps/pass-criteria under
  different literal test-data names) — covered by ELITEA-1794's merged test; this PR
  only added a second @allure.issue traceability decorator so the test's own coverage
  metadata links both TMS cases."
---

# ELITEA-1896: Export Agent with attached Skills — exported .md contains Skill content

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that exporting an agent with an attached Skill produces a .md file that includes the attached Skill's metadata and instructions.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill name | ExportSkill |
| Skill instructions | Export test instructions |
| Agent name | ExportAgent |
| Agent skill version | base |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill "ExportSkill" with instructions "Export test instructions" | "ExportSkill" is created successfully |
| 2 | Create an Agent "ExportAgent", attach "ExportSkill" (version: base) | "ExportAgent" is created with "ExportSkill" attached |
| 3 | Export "ExportAgent" as .md | A .md file is downloaded |
| 4 | Open the exported file and verify it contains the attached Skill's metadata and instructions | The file includes "ExportSkill" metadata and "Export test instructions" content |

---

## Expected Final State

The exported .md file contains the attached Skill's metadata (name, version) and its instructions content.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The exported .md file contains "ExportSkill" metadata and "Export test instructions".

**Fail:**
- Any step produces an error or unexpected result.
- The exported file is missing the Skill metadata or instructions.
