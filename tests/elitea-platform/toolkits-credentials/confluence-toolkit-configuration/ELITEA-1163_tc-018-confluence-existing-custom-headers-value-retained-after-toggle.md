---
id: ELITEA-1163
title: "TC-018 (Confluence): Existing Custom Headers Value Retained After Toggle Removal in Confluence Toolkit"
priority: medium
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1163: TC-018 (Confluence): Existing Custom Headers Value Retained After Toggle Removal in Confluence Toolkit

**Module:** Confluence Toolkit Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when an existing Confluence toolkit had a value saved in Custom Headers (previously via a toggle/expand mechanism), the Custom Headers value is still present and intact after the UI change removes the toggle and displays it flat. Data must not be silently dropped during the UI migration.

Coverage:
- Previously saved Custom Headers key-value pairs survive the removal of the toggle
- Data is visible in the flat Custom Headers field on reopen
- No data loss during UI format migration

## Preconditions

- An existing Confluence toolkit that had non-empty Custom Headers saved via the old toggle UI
- Logged in as the toolkit owner
- New UI (post-reorganization) deployed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pre-existing Confluence toolkit that had Custom Headers saved via the old toggle design | Toolkit form opens without error |
| 2 | Expand Advanced Settings | Advanced Settings expands; Custom Headers field visible (flat, no toggle) |
| 3 | Inspect the Custom Headers field | Previously saved Custom Headers key-value pairs are present and correctly displayed |
| 4 | Verify no data was silently emptied or truncated | All key-value entries that were saved are intact |

## Expected Final State

All key-value entries that were saved are intact

## Pass/Fail Criteria

PASS:
- Custom Headers values that were saved with the old toggle UI are still present after upgrade
- Values appear correctly in the flat Custom Headers field

FAIL:
- Custom Headers values are blank / lost after the UI change is deployed
- Key-value pairs that were saved previously are missing on reopen
