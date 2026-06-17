---
id: ELITEA-1198
title: "Jira Toolkit — Existing Toolkit Works Correctly After Hosting and API Version Migration"
priority: critical
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, int:jira, r-2.0.2]
requirements: []
---
# ELITEA-1198: Jira Toolkit — Existing Toolkit Works Correctly After Hosting and API Version Migration

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that existing Jira toolkits that were configured before the Hosting and API Version migration still work correctly — credentials are accessible, the toolkit opens without error, tool calls execute successfully, and the Cloud checkbox is no longer visible.

**Coverage:**
- Pre-existing Jira toolkit opens without errors after migration
- Cloud checkbox is no longer present in the toolkit configuration form
- The linked credential has a Hosting value set (migrated from the old cloud field)
- Tool calls on the existing toolkit still execute successfully (regression)

## Preconditions

- Logged in to {{base_url}}
- At least one Jira toolkit exists that was configured **before** the migration (i.e., it previously had a Cloud checkbox setting)
- The toolkit has a linked Jira credential with a valid Base URL and auth

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 2 | Open an existing Jira toolkit that was created before the Hosting/API Version migration. Inspect the toolkit configuration form. | The toolkit opens without errors. The **Cloud checkbox is absent** from the form. The API Version dropdown is present and shows a value (Auto, V2, or V3). |
| 3 | Navigate to the linked Jira credential. Inspect the Hosting field. | The Hosting field is present and shows a migrated value — not empty. If the old toolkit had `cloud: true`, Hosting should show **Cloud**; if `cloud: false` or not set, Hosting should show **Server** or **Auto** respectively. |
| 4 | Open the Jira toolkit Test Settings panel. Run a basic tool call (e.g., `list_projects` or `list_issues` with a valid project key). | The tool call executes successfully and returns results without errors. No regression introduced by the migration. |

## Expected Final State

The tool call executes successfully and returns results without errors. No regression introduced by the migration.

## Pass/Fail Criteria

**Pass:**
- Existing Jira toolkit opens without errors
- Cloud checkbox is absent from the toolkit form
- Linked credential has a non-empty Hosting value (Auto, Cloud, or Server)
- At least one tool call (e.g., list_projects or list_issues) executes without error

**Fail:**
- Existing toolkit fails to open or shows a config error
- Cloud checkbox is still present
- Tool calls fail with unexpected errors after migration
