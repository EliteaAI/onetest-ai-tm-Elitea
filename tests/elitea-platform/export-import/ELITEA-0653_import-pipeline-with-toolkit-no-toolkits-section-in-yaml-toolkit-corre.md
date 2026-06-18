---
id: ELITEA-0653
title: "Import Pipeline with Toolkit: No \"toolkits\" Section in YAML, Toolkit Correctly Attached"
priority: critical
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3824]
---
# ELITEA-0653: Import Pipeline with Toolkit: No "toolkits" Section in YAML, Toolkit Correctly Attached

**Module:** Export Import · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a pipeline with an attached toolkit is imported, the `toolkits` section is not persisted in the imported pipeline YAML, and the toolkit is correctly created/attached.

**Coverage:**
- Exported pipeline YAML contains a `toolkits` section (baseline confirmation)
- After import, the imported pipeline YAML does NOT contain a `toolkits` section
- The toolkit is correctly attached to the imported pipeline (created/linked during import, not a YAML remnant)

**Note:** Functional run verification is covered separately in TC-0733.

## Preconditions

- Logged in to {{base_url}} as Owner/Editor
- A source pipeline exists with at least one toolkit attached (e.g., GitHub toolkit or Confluence toolkit)
- The source pipeline contains at minimum: one Toolkit node (invoking the attached toolkit) and one LLM node
- The pipeline has been exported previously OR will be exported during the test — exported .yaml import file is available

## Test Data

- Source pipeline name: e.g., PipelineWithToolkit_Export
- Toolkit attached: GitHub toolkit (or any toolkit with at least one tool enabled)
- Toolkit node tool: e.g., get_file_contents or equivalent simple read operation
- Import file: the .yaml export of the above pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines → open the source pipeline that has a toolkit attached. Click Export / Download the import file. | Export succeeds; a .yaml file is downloaded to local machine. |
| 2 | Open the downloaded export file in a text editor. Search for the `toolkits:` key in the YAML content. | Baseline confirmed: The exported file DOES contain a `toolkits:` section listing the attached toolkit(s). |
| 3 | Navigate to Pipelines → Import. Select the downloaded file and confirm the import. | Import process completes without error; a new imported pipeline appears in the pipeline list. |
| 4 | Open the imported pipeline → navigate to the YAML/configuration source view (e.g., Edit YAML or raw config view). | Imported pipeline opens; YAML is visible. |
| 5 | Search the imported pipeline YAML for the `toolkits:` key. | The `toolkits:` section is NOT present in the imported pipeline YAML. The YAML structure matches the exported YAML minus the `toolkits` section. |
| 6 | Open the imported pipeline's Toolkits / configuration panel and check which toolkits are listed. | The toolkit (e.g., GitHub toolkit) IS listed and attached to the imported pipeline — it was created/linked during the import process, not left as a YAML remnant. |

## Expected Final State

The toolkit (e.g., GitHub toolkit) IS listed and attached to the imported pipeline — it was created/linked during the import process, not left as a YAML remnant.

## Pass/Fail Criteria

**Pass:**
- Exported YAML contains a `toolkits:` section (baseline confirmed at step 2)
- Imported pipeline YAML does NOT contain a `toolkits:` section (step 5)
- Toolkit IS correctly attached to the imported pipeline (step 6)

**Fail:**
- Imported pipeline YAML still contains a `toolkits:` section after import
- Toolkit is missing/not attached to the imported pipeline
- Exported and imported YAML differ in sections other than `toolkits`
