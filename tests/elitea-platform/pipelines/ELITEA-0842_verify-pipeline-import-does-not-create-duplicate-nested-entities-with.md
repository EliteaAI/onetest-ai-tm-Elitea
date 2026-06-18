---
id: ELITEA-0842
title: "Verify pipeline import does not create duplicate nested entities with multiple versions"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0842: Verify pipeline import does not create duplicate nested entities with multiple versions

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** When importing pipelines that have multiple versions in their hierarchy, the import process creates duplicate nested entities (agents, toolkits, etc.) that are attached to the pipeline. This test extends beyond basic import (covered in TC-0049) to verify correct handling of multi-version pipeline hierarchies during import.

## Preconditions

User logged into Elitea stage.elitea.ai
A source pipeline exists with:
  - Multiple versions (at least 2 versions)
  - Nested entities: agent nodes referencing existing agents, toolkit associations
  - The pipeline hierarchy includes shared entities across versions
Access to the pipeline export file (.md or .json format)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to an existing pipeline with multiple versions and nested entities. Document the exact count of nested entities (agents, toolkits) across all versions | Pipeline details show the exact number of nested agents and toolkits. For example: Version 1 has Agent A + Toolkit X, Version 2 has Agent A + Agent B + Toolkit X |
| 2 | Export the pipeline using the three-dot menu > Export | Pipeline export file is downloaded successfully containing all versions and nested entity references |
| 3 | Navigate to the Pipelines list page and import the exported file via the Import functionality | Import wizard processes the file and shows the pipeline to be imported with its versions and dependencies |
| 4 | Complete the import process | Pipeline is imported successfully without errors |
| 5 | Open the imported pipeline and navigate to Version 1. Count the nested entities (agents, toolkits) | Version 1 has exactly the same number of nested entities as the original — no duplicates. Agent A appears once, Toolkit X appears once |
| 6 | Switch to Version 2 of the imported pipeline. Count the nested entities | Version 2 has exactly the same number of nested entities as the original — no duplicates. Shared entities (Agent A, Toolkit X) are not duplicated |
| 7 | Check the Agents and Toolkits pages to verify no duplicate agents or toolkits were created during import | No duplicate agents or toolkits exist. Shared entities are referenced, not duplicated |
| 8 | Execute the imported pipeline to verify nested entities function correctly without duplication issues | Pipeline executes correctly. Agent nodes reference the correct agents. No errors from duplicate entity conflicts |
| 9 | Import the same exported file a second time (re-import) and check if additional duplicates are created | Second import either merges with the existing imported pipeline or creates a new pipeline with a conflict name — but does NOT create additional duplicate nested entities (agents, toolkits). Entity count on Agents/Toolkits pages does not increase |
| 10 | Delete the imported pipeline and verify that the nested entities (agents, toolkits) that were shared with other pipelines or the original are NOT cascade-deleted | Deleting the imported pipeline does not remove shared agents or toolkits that are still referenced by other entities. The original pipeline and its nested entities remain intact |
| 11 | Re-import the pipeline file one more time and compare the imported pipeline's node configuration with the original to verify all node settings, connections, and entity references are identical | Imported pipeline is a faithful copy of the original — all node configurations, edge connections, entity references, and version structures match exactly. No data loss or corruption during import/export roundtrip |
| 12 | Open the imported pipeline in YAML view and compare with the original pipeline's YAML to verify structural equivalence | YAML representations are structurally equivalent (node definitions, edges, entity IDs may differ but structure and configuration values match). No extra or missing entity references in the YAML |

## Expected Final State

YAML representations are structurally equivalent (node definitions, edges, entity IDs may differ but structure and configuration values match). No extra or missing entity references in the YAML

## Pass/Fail Criteria

PASS: Imported pipeline has identical entity counts to the original across all versions; no duplicate nested agents or toolkits are created; re-import does not multiply duplicates; deletion does not cascade-remove shared entities; YAML structures match
FAIL: Import creates duplicate nested entities, entity counts differ from original, re-import multiplies duplicates, deletion cascades to shared entities, or structural differences found in YAML comparison
