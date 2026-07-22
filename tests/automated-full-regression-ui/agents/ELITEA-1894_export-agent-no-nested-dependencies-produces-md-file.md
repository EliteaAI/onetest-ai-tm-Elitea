---
id: ELITEA-1894
title: "Export agent with no nested dependencies — produces .md file with correct content"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.skills.test_export_agent_no_nested_dependencies.TestExportAgentNoNestedDependencies.test_export_agent_no_nested_dependencies
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/514
---

# ELITEA-1894: Export agent with no nested dependencies — produces .md file with correct content

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that exporting an agent with no nested agent dependencies produces a .md file containing the correct YAML frontmatter (name, description, model settings, instructions) and no sensitive credentials.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with no nested agent dependencies is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent with no nested agent dependencies | The agent detail page loads |
| 2 | Select the version to export from the version dropdown | The desired version is selected |
| 3 | Click the three-dot menu (⋮) → select "Export" | The export action is triggered |
| 4 | Verify a .md file is downloaded automatically | A .md file download is initiated |
| 5 | Open the file and verify it contains YAML frontmatter with: name, description, model settings (model, max_tokens, agent_type, step_limit), instructions body | The file includes all required YAML frontmatter fields. **Note**: `temperature` is NOT included for reasoning-capable models (platform behavior as of 2026-07-22, refs EliteaAI/elitea_issues#5821) |
| 6 | Verify the file does NOT contain any toolkit API keys or authentication credentials | No API keys or credentials are present in the exported file |

---

## Expected Final State

The exported .md file contains correct YAML frontmatter (name, description, model settings, instructions) and no sensitive credentials.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The .md file is downloaded with correct frontmatter and no credentials.

**Fail:**
- Any step produces an error or unexpected result.
- The file is not downloaded, is in the wrong format, is missing required fields, or contains sensitive credentials.
