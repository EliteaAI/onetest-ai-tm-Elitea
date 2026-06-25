---
id: ELITEA-0142
title: "Agent Export and Import"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - test_export_import_prompts.py:TestExportImportRoundtrip.test_export_import_roundtrip_basic
  - test_export_import_prompts.py:TestExportImportRoundtrip.test_export_import_preserves_all_fields
  - test_export_import_prompts.py:TestExportImportConflicts.test_import_with_conflicting_name_creates_new
tags: []
requirements: []
---
# ELITEA-0142: Agent Export and Import

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that agents can be exported to YAML, imported back, and all fields are preserved. Test conflict handling when importing duplicate names.

## Preconditions

- User logged into Elitea
- Test agent exists
- Export/Import UI available

## Test Data

- URL: {{base_url}}
- Export format: YAML with frontmatter

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Export agent to YAML | YAML file downloaded |
| ? | Import YAML file | Agent recreated with same properties |
| ? | Import same file again | New agent created with conflict suffix |

## Expected Final State

New agent created with conflict suffix

## Pass/Fail Criteria

**Pass:**
- Export produces valid YAML
- Import recreates agent correctly
- All fields match original
- Conflict creates new agent

**Fail:**
- Export fails
- Import corrupts data
- Fields lost
- Conflict overwrites
