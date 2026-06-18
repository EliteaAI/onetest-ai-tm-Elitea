---
id: ELITEA-0861
title: "Pipeline Export and Import"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - test_export_import_pipelines.py:TestPipelineExportImportRoundtrip.test_pipeline_export_import_roundtrip_basic
test_export_import_pipelines.py:TestPipelineExportImportRoundtrip.test_pipeline_export_import_preserves_all_fields
test_export_import_pipelines.py:TestPipelineExportImportEdgeCases.test_pipeline_export_import_complex_topology
tags: []
requirements: []
---
# ELITEA-0861: Pipeline Export and Import

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that pipelines can be exported to YAML, imported back with all fields and topology preserved, including complex multi-node pipelines.

## Preconditions

- User logged into Elitea
- Test pipeline with multiple nodes exists

## Test Data

- URL: {{base_url}}
- Export format: YAML with flow definition

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Export pipeline to YAML | YAML file downloaded with nodes/edges |
| ? | Import YAML file | Pipeline recreated with same topology |
| ? | Verify nodes and connections | All nodes present, connections intact |

## Expected Final State

All nodes present, connections intact

## Pass/Fail Criteria

**Pass:**
- Export produces valid YAML
- Import recreates pipeline
- All nodes and connections preserved
- Complex topology intact

**Fail:**
- Export fails
- Nodes lost
- Connections broken
- Topology corrupted
