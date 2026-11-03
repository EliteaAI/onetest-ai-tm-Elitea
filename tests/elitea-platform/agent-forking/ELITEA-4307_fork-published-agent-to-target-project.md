---
id: ELITEA-4307
title: "Fork published agent to target project succeeds"
priority: critical
type: functional
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- User is logged into `{{base_url}}`
- At least one agent is published to the Catalog
- User has access to a target project different from the published agent's source

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Any published agent in Catalog/Agent Hub |
| Target Project | testproj1 (or any project different from source) |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog/Agent Hub in `{{base_url}}/app/` | Catalog loads; published agents list visible |
| 2 | Select a published agent from the list | Agent details displayed; Fork button visible |
| 3 | Click the Fork button | Fork dialog appears with project selector |
| 4 | Select target project (testproj1) from dropdown | Target project name displayed in dialog |
| 5 | Click Confirm button | Fork request submitted; HTTP 200 response received |
| 6 | Wait for fork completion | Redirect to target project or success confirmation shown |
| 7 | Navigate to target project (testproj1) | Project loads; agents list displayed |
| 8 | Verify forked agent appears in agent list | Forked agent visible with unique ID |
| 9 | Open the forked agent | Agent details load with all data: name, description, version history, toolkits intact |
| 10 | Attempt to execute or edit the forked agent | Agent can be executed or edited without errors |

## Expected Final State

- Forked agent exists independently in target project with unique ID
- Forked agent retains all original data (name, description, metadata, toolkits, versions)
- Forked agent is fully functional (can be executed, edited, re-forked)

## Pass/Fail Criteria

**Pass:**
- Fork operation completes with HTTP 200 (or success response)
- Forked agent appears in target project with unique ID
- All agent data is present and intact
- Forked agent is functional (executable and editable)

**Fail:**
- Fork fails with HTTP 4xx or 5xx error
- Forked agent does not appear in target project
- Forked agent has missing or corrupted data
- Forked agent cannot be executed or edited
