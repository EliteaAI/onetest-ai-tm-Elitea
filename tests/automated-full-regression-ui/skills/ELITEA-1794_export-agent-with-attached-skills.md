---
id: ELITEA-1794
title: "Export Agent with attached Skills — exported .md contains Skill content"
priority: high
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: automation/tests/ui/skills/test_export_agent_with_attached_skills.py::TestExportAgentWithAttachedSkills::test_export_agent_with_attached_skills
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/53
---

# ELITEA-1794: Export Agent with attached Skills — exported .md contains Skill content

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that when an Agent with attached Skills is exported, the resulting `.md` file contains the Skill content (instructions, name, version) embedded in the export, not merely a reference.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- An Agent exists with at least one Skill attached.
- The Agent export feature is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | (any Agent with at least one Skill attached, e.g. "Export Test Agent") |
| Attached Skill name | (e.g., "Formatter") |
| Attached Skill instructions | (known instructions text to verify in export) |
| Expected export format | `.md` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents and open the Agent with attached Skills | Agent detail or edit view is open |
| 2 | Trigger the Export action for the Agent | A file download is initiated |
| 3 | Verify the exported file has a `.md` extension | Downloaded file is a `.md` file |
| 4 | Open the exported `.md` file and inspect its contents | File contents are readable |
| 5 | Verify the Skill name is present in the exported content | The attached Skill's name appears in the file |
| 6 | Verify the Skill instructions/content are present in the exported file | The Skill's instruction text (not just its ID or name reference) is embedded in the export |
| 7 | Verify the Skill version is indicated in the exported file | The Skill version (e.g., `base`) is present in the file |

---

## Expected Final State

The exported `.md` file contains full Skill content — including name, version, and instructions — embedded directly in the file, enabling a self-contained Agent export that can be imported elsewhere.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Exported file is `.md` format.
- Skill name, instructions, and version are all present in the exported file content.

**Fail:**
- Any step produces an error or unexpected result.
- Exported file is missing Skill content (only contains a reference or ID instead of full content).
- Exported file is not `.md` format.
