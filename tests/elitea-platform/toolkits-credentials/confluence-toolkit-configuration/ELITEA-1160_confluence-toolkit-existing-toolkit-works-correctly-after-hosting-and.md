---
id: ELITEA-1160
title: "Confluence Toolkit — Existing Toolkit Works Correctly After Hosting and API Version Migration"
priority: critical
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, r-2.0.2]
requirements: []
---
# ELITEA-1160: Confluence Toolkit — Existing Toolkit Works Correctly After Hosting and API Version Migration

**Module:** Confluence Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that existing Confluence toolkits that were configured before the Hosting and API Version migration still work correctly — credentials are accessible, the toolkit opens without error, tool calls execute successfully, and the Cloud checkbox is no longer visible.

**Coverage:**
- Pre-existing Confluence toolkit opens without errors after migration
- Cloud checkbox is no longer present in the toolkit configuration form
- The linked credential has a Hosting value set (migrated from the old cloud field)
- Tool calls on the existing toolkit still execute successfully (regression)

## Preconditions

- Logged in to {{base_url}}
- At least one Confluence toolkit exists that was configured **before** the migration (i.e., it previously had a Cloud checkbox setting)
- The toolkit has a linked Confluence credential with a valid Base URL and auth

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 2 | Open an existing Confluence toolkit that was created before the Hosting/API Version migration. Inspect the toolkit configuration form. | The toolkit opens without errors. The **Cloud checkbox is absent** from the form. The API Version dropdown is present and shows a value (Auto, V2, or V3). |
| 3 | Navigate to the linked Confluence credential. Inspect the Hosting field. | The Hosting field is present and shows a migrated value — not empty. If the old toolkit had `cloud: true`, Hosting should show **Cloud**; if `cloud: false` or not set, Hosting should show **Server** or **Auto** respectively. |
| 4 | Open the Confluence toolkit Test Settings panel. Run a basic tool call (e.g., `get_page` or `search_pages` with a valid space/page). | The tool call executes successfully and returns results without errors. No regression introduced by the migration. |

## Expected Final State

The tool call executes successfully and returns results without errors. No regression introduced by the migration.

## Pass/Fail Criteria

**Pass:**
- Existing Confluence toolkit opens without errors
- Cloud checkbox is absent from the toolkit form
- Linked credential has a non-empty Hosting value (Auto, Cloud, or Server)
- At least one tool call (e.g., get_page or search_pages) executes without error

**Fail:**
- Existing toolkit fails to open or shows a config error
- Cloud checkbox is still present
- Tool calls fail with unexpected errors after migration
