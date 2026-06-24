---
id: ELITEA-1704
title: Verify existing agents configured with PGVector credentials continue to work after changes
priority: critical
type: regression
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1704: Verify existing agents configured with PGVector credentials continue to work after changes

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that existing agents with PGVector configuration remain fully functional after the UI changes, with no data loss or need for reconfiguration (regression test).


## Preconditions

- At least one agent exists with PGVector configuration already set up
- PGVector credential (e.g., "elitea-pgvector") is configured for the agent
- User has access to view/edit the agent

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Agent | [existing agent with PGVector] |
| Expected Credential | elitea-pgvector |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Agents page loads |
| 2 | Open an existing agent that has PGVector configured | Agent configuration page loads without errors |
| 3 | Expand "Toolkit" section | Toolkit section expands |
| 4 | Verify PGVector Configuration field | Field displays the previously selected credential (e.g., "elitea-pgvector") |
| 5 | Check all agent settings | All settings are intact and unchanged |
| 6 | Click "Save" button (without making changes) | Agent saves successfully without errors or warnings |
| 7 | Check browser console | No JavaScript errors appear |

## Expected Final State

Existing agents with PGVector configuration remain fully functional with no data loss or corruption after UI changes.

## Pass/Fail Criteria

**Pass:**
- Agent configuration loads successfully
- PGVector Configuration displays previously selected credential
- No errors or warnings appear in UI
- Agent can be saved without reconfiguration
- No data loss or corruption
- No JavaScript errors in console

**Fail:**
- Agent configuration fails to load
- PGVector credential is missing or reset
- Errors or warnings appear
- Agent cannot be saved
- Agent settings are corrupted
- JavaScript errors occur
