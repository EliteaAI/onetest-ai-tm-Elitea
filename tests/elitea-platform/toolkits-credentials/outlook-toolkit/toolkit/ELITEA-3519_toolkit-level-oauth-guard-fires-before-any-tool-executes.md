---
id: ELITEA-3519
title: "Toolkit-Level OAuth Guard Fires Before Any Tool Executes"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3519: Toolkit-Level OAuth Guard Fires Before Any Tool Executes

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify a toolkit linked to an unauthorized (never-logged-in) Outlook credential blocks all tool execution with a clear OAuth-required message, rather than letting the call reach Graph and fail unpredictably.

## Preconditions

- A newly created Outlook credential that has never completed OAuth login
- A toolkit created using that unauthorized credential

## Test Data

- Toolkit: `outlook-toolkit-unauth`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create an Outlook credential and do not authorize it | Credential exists, unauthorized |
| 2 | Create a toolkit `outlook-toolkit-unauth` using this credential | Toolkit is created |
| 3 | Assign the toolkit to an agent and invoke any tool (e.g. `list_folders`) | Tool call is blocked before reaching Graph; a clear "OAuth required / not authorized" message is returned to the agent/user |

## Expected Final State

No Graph API call is made; the user receives a clear, actionable OAuth-required message.

## Pass/Fail Criteria

**Pass:**
- Tool execution is blocked pre-flight with a clear OAuth-required message

**Fail:**
- The call reaches Graph and fails with an unrelated/unclear error
- The tool executes successfully despite no authorization
