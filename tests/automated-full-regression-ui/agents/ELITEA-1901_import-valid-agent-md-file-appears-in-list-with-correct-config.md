---
id: ELITEA-1901
title: "Import valid agent .md file — agent appears in list with correct config"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_import_agent_valid_md_file.TestImportAgentValidMdFile.test_import_agent_valid_md_file
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/629
---

# ELITEA-1901: Import valid agent .md file — agent appears in list with correct config

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that importing a valid .md file with correct YAML frontmatter creates an agent that appears in the Agents dashboard with matching Name, Description, and Instructions.

---

## Preconditions

- User is logged in to the Elitea platform.
- A valid .md file with YAML frontmatter (name, description, model settings and the Agent's instructions as the markdown body below the frontmatter) is available for import.

---

## Test Data

| Field | Value |
|-------|-------|
| Import file | Valid .md file with YAML frontmatter: name, description, model + instructions as markdown body |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Agents dashboard | The Agents dashboard loads |
| 2 | Click the "Import" button | The import dialog or file picker opens |
| 3 | Upload a valid .md file with correct YAML frontmatter (name, description, model, instructions) | The file is uploaded and processed |
| 4 | Verify the import wizard shows the entity card for the agent | An entity card for the agent is displayed in the wizard |
| 5 | Click Confirm/Import | The import operation completes |
| 6 | Verify the agent appears in the Agents dashboard with the correct name | The imported agent is visible in the dashboard with the correct name |
| 7 | Open the imported agent — verify Name, Description, and Instructions match the file content | All three fields match the imported file content |

---

## Expected Final State

The imported agent is visible in the Agents dashboard and its Name, Description, and Instructions all match the content of the imported .md file.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The imported agent appears in the dashboard with matching Name, Description, and Instructions.

**Fail:**
- Any step produces an error or unexpected result.
- The agent does not appear in the dashboard, or its fields do not match the imported file content.
