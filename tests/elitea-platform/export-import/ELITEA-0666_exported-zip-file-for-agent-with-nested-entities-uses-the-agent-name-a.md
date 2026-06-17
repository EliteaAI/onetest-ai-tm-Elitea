---
id: ELITEA-0666
title: "Exported ZIP file for Agent with nested entities uses the Agent name as filename"
priority: medium
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:agents, R-2.0.1, eng:ui]
requirements: [ProjectAlita/projectalita.github.io#3725]
---
# ELITEA-0666: Exported ZIP file for Agent with nested entities uses the Agent name as filename

**Module:** Export Import · **Priority:** Medium · **Type:** Functional

**Objective:** Objective:
Verify that exporting an Agent containing nested entities downloads a ZIP file whose filename matches the Agent name so exported files are easily identifiable.

Coverage:
- Export an Agent that contains nested entities (sub-agents or toolkits)
- Confirm that a ZIP file is downloaded when Export is invoked
- Confirm the downloaded ZIP filename matches the Agent name with the `.zip` extension

## Preconditions

- User is logged in to the application.
- User has permission to view Agents and export Agents.
- An Agent named `test-agent-export` is created and contains at least one nested entity (sub-agent or toolkit).
- User has access to the browser Downloads folder to inspect downloaded files.

## Test Data

Agent name: `test-agent-export`
Expected filename: `test-agent-export.zip`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page | Agents list loads and displays test-agent-export. |
| 2 | Open the Agent named test-agent-export | Agent editor opens for test-agent-export |
| 3 | Click the Export button in the Agent editor and confirm export if a modal appears. | Export process starts and a ZIP file is downloaded. |
| 4 | Inspect the downloaded file name in the Downloads folder. | The downloaded file name is test-agent-export.zip. |

## Expected Final State

The downloaded file name is test-agent-export.zip.

## Pass/Fail Criteria

Pass:
- A ZIP file is downloaded successfully.
- The downloaded ZIP filename matches `test-agent-export.zip`.

Fail:
- No ZIP file is downloaded.
- The downloaded ZIP filename does not match `test-agent-export.zip` (e.g., `alita_export_YYYY-MM-DD.zip` or another generic name).
