---
id: ELITEA-0139
title: "Agent Export and Import - YAML Format"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.agents.test_export_import_prompts.TestExportImportRoundtrip.test_export_import_roundtrip_basic
  - tests.ui.agents.test_export_import_prompts.TestExportImportRoundtrip.test_export_import_preserves_all_fields
  - tests.ui.agents.test_export_import_prompts.TestExportImportRoundtrip.test_export_format_is_valid_yaml_frontmatter
  - tests.ui.agents.test_export_import_prompts.TestExportImportConflicts.test_import_preserves_original_when_conflict
  - tests.ui.agents.test_export_import_prompts.TestExportImportConflicts.test_import_with_conflicting_name_creates_new
  - tests.ui.agents.test_export_import_prompts.TestExportImportEdgeCases.test_export_import_empty_optional_fields
  - tests.ui.agents.test_export_import_prompts.TestExportImportEdgeCases.test_export_import_special_characters_in_name
  - tests.ui.agents.test_export_import_prompts.TestExportImportEdgeCases.test_export_import_large_instructions
  - tests.ui.agents.test_export_import_prompts.TestExportImportEdgeCases.test_import_via_constructed_payload
tags: []
requirements: []
---
# ELITEA-0139: Agent Export and Import - YAML Format

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that agents can be exported to `.agent.md` YAML format and imported back with full field preservation, including conflict handling.

**Coverage:**
- Export agent to `.agent.md` with YAML frontmatter
- Import agent from YAML file
- Verify all fields preserved (variables, description, welcome_message, conversation_starters, tags)
- Handle conflicting names on import (creates new agent)
- Edge cases: empty optional fields, special characters, large instructions

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one agent exists for export testing (create one manually if needed with a name, description, and instructions)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Test user: alita@elitea.ai
- Agent to export should have: name, description, instructions, and optionally variables/tags
- Special characters test name: agent with & @ - in name
- Large instructions test: agent with 5000+ characters of instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page and create a new agent (or use an existing one) with a name, description, instructions, and optionally variables. | Agent is created and visible on the Agents dashboard. |
| 2 | Open the agent's detail page. Click the three-dot menu (top right) and select 'Export'. | A file downloads with .agent.md extension containing YAML frontmatter (starts with '---') followed by the agent instructions. |
| 3 | Open the downloaded .agent.md file in a text editor. Verify it contains YAML frontmatter with keys like 'name', 'model', and 'agent_type'. | The YAML content is valid. Required keys (name, model, agent_type) are present. |
| 4 | Delete the original agent. Then navigate to the Agents page and use the Import function to upload the .agent.md file. | Import succeeds. A new agent is created from the imported file. |
| 5 | Open the imported agent and compare all fields (name, description, instructions, model, temperature, variables) with the original values. | All fields match the original agent values. |
| 6 | Without deleting the imported agent, import the same .agent.md file again. | A second agent is created with the same name. The original imported agent is unchanged. |
| 7 | Test edge cases: export/import an agent with special characters in the name (e.g., & @ -), and another with very long instructions (5000+ characters). | Special characters survive the roundtrip intact. Long instructions are preserved without truncation. |

## Expected Final State

Special characters survive the roundtrip intact. Long instructions are preserved without truncation.

## Pass/Fail Criteria

**Pass:**
- Export produces valid YAML frontmatter format
- Import creates agent with all fields preserved
- Conflict import creates second agent without affecting original
- Special characters survive roundtrip
- Large instructions (5000+ chars) roundtrip without data loss

**Fail:**
- Export returns empty or invalid YAML
- Import fails or loses field values
- Conflict import overwrites original agent
- Special characters corrupted during roundtrip
- Large instructions truncated or corrupted
