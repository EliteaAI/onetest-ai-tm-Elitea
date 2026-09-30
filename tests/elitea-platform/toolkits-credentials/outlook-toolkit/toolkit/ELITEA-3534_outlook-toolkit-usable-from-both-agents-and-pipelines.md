---
id: ELITEA-3534
title: "Outlook Toolkit Usable From Both Agents and Pipelines"
priority: high
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3534: Outlook Toolkit Usable From Both Agents and Pipelines

**Module:** Outlook Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify the Outlook toolkit can be attached to and successfully invoked from both an Agent and a Pipeline.

## Preconditions

- An authorized Outlook credential and toolkit (per ELITEA-3517)
- An existing Agent and an existing Pipeline in the project

## Test Data

- Agent: existing test agent
- Pipeline: existing test pipeline with a step that can call a toolkit tool

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Assign the Outlook toolkit to the test Agent and invoke `list_messages` from agent chat | Tool executes successfully, returns messages |
| 2 | Assign the Outlook toolkit to the test Pipeline and configure a step to call `list_folders` | Pipeline step is configured successfully |
| 3 | Run the Pipeline | Pipeline executes the Outlook step successfully and returns folder data |

## Expected Final State

The Outlook toolkit functions correctly when invoked from both consumer types.

## Pass/Fail Criteria

**Pass:**
- Both Agent and Pipeline invocations succeed and return correct data

**Fail:**
- Toolkit works from one consumer but fails or is unavailable from the other
