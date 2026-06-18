---
id: ELITEA-0675
title: "Fork Excludes Credentials and Shows Warning to Re-Enter"
priority: critical
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0675: Fork Excludes Credentials and Shows Warning to Re-Enter

**Module:** Fork · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that credentials (API keys, tokens, passwords) are never copied to the forked entity and the user receives a warning to re-enter them.

**Coverage:**
- Credential exclusion during fork
- User warning about missing sensitive data
- Forked agent editability for manual credential entry

## Preconditions

- Logged in as Editor in Source Project and Target Project
- Source Project has an agent with an active Toolkit that has an API key/token configured

## Test Data

- Agent with toolkit: any agent with a credential-configured toolkit (e.g. GitHub, Jira toolkit)
- Credential field to check: API key or token field in the toolkit settings

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Source Project → Agents, open the agent with a credential-configured toolkit | Agent opens, toolkit is visible with credentials set |
| 2 | Initiate Fork → select Target Project → confirm | Fork completes; "Fork Complete" shown |
| 3 | Navigate to Target Project → Agents → open the forked agent | Forked agent opens |
| 4 | Navigate to the forked agent's toolkit/tool configuration | Toolkit configuration panel is visible |
| 5 | Inspect credential fields (API key, token, password) | All credential fields are empty/blank if the default credentials are not available |
| 6 | Check for a warning message about missing credentials | Warning is displayed indicating sensitive data was not copied and must be re-entered |
| 7 | Attempt to edit and save a credential in the forked agent | Edit saves successfully; agent remains functional |

## Expected Final State

Edit saves successfully; agent remains functional

## Pass/Fail Criteria

**Pass:**
- All credential fields in the forked toolkit are blank
- Warning message about excluded sensitive data is shown
- Forked agent is editable and accepts new credentials

**Fail:**
- Any credential field is pre-populated with data from the source
- No warning is displayed about missing credentials
- Forked agent is not editable
