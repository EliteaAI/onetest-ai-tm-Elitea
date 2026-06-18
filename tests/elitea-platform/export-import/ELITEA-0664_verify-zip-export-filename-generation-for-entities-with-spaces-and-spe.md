---
id: ELITEA-0664
title: "Verify ZIP export filename generation for entities with spaces and special characters"
priority: medium
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:pipelines, feat:agents, regression, R-2.0.1, eng:ui]
requirements: [ProjectAlita/projectalita.github.io#3725]
---
# ELITEA-0664: Verify ZIP export filename generation for entities with spaces and special characters

**Module:** Export Import · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when exporting an Agent or Pipeline containing nested entities, the generated ZIP filename is derived from the entity name and sanitized correctly when the name contains spaces or special characters.

Coverage
- Export Agent with nested entities (ZIP export)
- Export Pipeline with nested entities (ZIP export)
- Verify ZIP filename is derived from entity name
- Verify spaces are converted to hyphens
- Verify special characters are removed or sanitized
- Verify fallback filename is used if entity name contains only unsupported characters

## Preconditions

- User is logged in to the application.
- User has permission to view and export Agents and Pipelines.
- Test entities with nested elements are created so that export produces a ZIP archive:
- Agent with nested entities
- Pipeline with nested entities
- User has access to the browser Downloads folder.

## Test Data

| Entity Type       | Entity Name      | Expected ZIP Filename |
| ----------------- | ---------------- | --------------------- |
| Agent             | My Test Agent v2 | my-test-agent-v2.zip  |
| Pipeline          | Agent:résumé/测试  | agent-resume.zip      |
| Agent or Pipeline | !№;%:            | zip.zip               |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agents page. | Agents list loads successfully. |
| 2 | Create/Open the Agent named "My Test Agent v2". (with nested Agent/Pipeline) | Agent editor opens. |
| 3 | Click Export. | Export process starts and a ZIP file is downloaded. |
| 4 | Inspect the downloaded filename. | Filename equals my-test-agent-v2.zip. |
| 5 | Open the Pipelines page. | Pipelines list loads successfully. |
| 6 | Create/Open the Pipeline named "Agent:résumé/测试". (with nested Agent/Pipeline) | Pipeline editor opens. |
| 7 | Click Export. | ZIP archive is downloaded. |
| 8 | Inspect the downloaded filename. | Filename equals agent-resume.zip (sanitized). |
| 9 | Create/Open an entity named "!№;%:" (Agent or Pipeline). (with nested Agent/Pipeline) | Entity editor opens. |
| 10 | Click Export. | ZIP archive is downloaded. |
| 11 | Inspect the downloaded ZIP. | Filename equals zip.zip (fallback filename). |

## Expected Final State

Filename equals zip.zip (fallback filename).

## Pass/Fail Criteria

Pass
- ZIP archive is downloaded for each export.
- Filename is derived from the entity name.
- Spaces are replaced with hyphens.
- Unsupported characters are sanitized.
- Fallback filename zip.zip is used when entity name contains only unsupported characters.

Fail
- ZIP archive is not downloaded.
- Filename is unrelated to entity name.
- Filename contains invalid filesystem characters.
- Fallback filename is not applied when required.
