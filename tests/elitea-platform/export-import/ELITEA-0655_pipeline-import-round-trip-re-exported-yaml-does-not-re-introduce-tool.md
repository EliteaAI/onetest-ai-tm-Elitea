---
id: ELITEA-0655
title: "Pipeline Import Round-Trip: Re-Exported YAML Does Not Re-Introduce toolkits Section"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3824]
---
# ELITEA-0655: Pipeline Import Round-Trip: Re-Exported YAML Does Not Re-Introduce toolkits Section

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that after a pipeline with toolkits is imported, re-exporting the imported pipeline produces a YAML that does not contain a `toolkits:` section and is structurally identical to the original export.

**Coverage:**
- Original export YAML contains a `toolkits:` section (baseline)
- Imported pipeline YAML does not contain `toolkits:` section (import fix in effect)
- Re-exporting the imported pipeline does NOT re-introduce the `toolkits:` section
- Re-exported YAML is structurally identical to the original exported YAML (round-trip parity)
- Idempotency: second-generation import of the re-export also produces a clean YAML
- Ensures the fix is not superficial (not just stripped at display layer but persisted correctly)

## Preconditions

- Logged in to {{base_url}} as Owner/Editor
- A source pipeline exists with at least one toolkit attached (e.g., GitHub or Confluence toolkit)
- The source pipeline has been exported as a .yaml file — this file is the reference export

## Test Data

- Source pipeline name: e.g., PipelineWithToolkit_RoundTrip
- Toolkit attached: any standard toolkit (e.g., GitHub toolkit)
- Reference export file: original_export.yaml (downloaded from the source pipeline)
- Imported pipeline name: e.g., PipelineWithToolkit_RoundTrip_Imported
- Re-export file: reimport_export.yaml (downloaded from the imported pipeline)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open original_export.yaml in a text editor. Search for the `toolkits:` key. | Baseline confirmed: The original export file contains a `toolkits:` section. Note the full YAML structure for reference. |
| 2 | Navigate to Pipelines → Import. Select original_export.yaml and confirm the import. | Import completes without error; imported pipeline appears in the pipeline list. |
| 3 | Open the imported pipeline's YAML/configuration source view. Search for `toolkits:`. | Imported pipeline YAML does NOT contain a `toolkits:` section. |
| 4 | With the imported pipeline open, click Export / download the import file for this imported pipeline. Save as reimport_export.yaml. | Export succeeds; reimport_export.yaml is downloaded. |
| 5 | Open reimport_export.yaml in a text editor. Search for the `toolkits:` key. | `toolkits:` section is NOT present in reimport_export.yaml. The re-exported YAML does not re-introduce the toolkits section. |
| 6 | Compare original_export.yaml and reimport_export.yaml structure side-by-side (excluding the `toolkits:` section from the original). Check all other top-level keys, node definitions, states, and connections. | The two files are structurally identical in all sections outside of `toolkits:`. No unexpected keys added or removed. Node count, types, connections, and config values match. |
| 7 | Import reimport_export.yaml a second time to verify idempotency. | Import succeeds again. The second-generation imported pipeline's YAML also does not contain a `toolkits:` section. |
| 8 | Verify the toolkit is correctly attached on both the first-generation and second-generation imported pipelines (check Toolkits panel). | Both imported pipelines show the toolkit correctly attached/listed, confirming toolkits were created from the YAML during each import. |

## Expected Final State

Both imported pipelines show the toolkit correctly attached/listed, confirming toolkits were created from the YAML during each import.

## Pass/Fail Criteria

**Pass:**
- Original export contains `toolkits:` section (step 1 — baseline confirmed)
- Imported pipeline YAML does not contain `toolkits:` section (step 3)
- Re-exported YAML does not contain `toolkits:` section (step 5)
- Re-exported YAML is structurally identical to the original export minus the `toolkits:` section (step 6)
- Second-generation import also produces a clean YAML (step 7)
- Toolkit is attached on all imported pipelines (step 8)

**Fail:**
- Re-exported YAML re-introduces the `toolkits:` section (reveals fix is only at import display layer)
- Re-exported YAML differs from the original in sections beyond `toolkits:` (data loss or mutation)
- Toolkit is missing from the imported pipeline after idempotent re-import
