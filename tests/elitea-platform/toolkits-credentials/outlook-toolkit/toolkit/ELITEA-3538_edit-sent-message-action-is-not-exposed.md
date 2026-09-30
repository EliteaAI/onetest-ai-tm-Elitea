---
id: ELITEA-3538
title: "Edit-Sent-Message Action Is Not Exposed"
priority: high
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3538: Edit-Sent-Message Action Is Not Exposed

**Module:** Outlook Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify there is no tool to edit an already-sent message, per the issue's explicit out-of-scope statement (Microsoft Graph does not support this).

## Preconditions

- Toolkit with all 12 tools enabled

## Test Data

- N/A (negative/absence check)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enumerate the full list of available tools in the TOOLS section with no `selected_tools` restriction | Exactly the 12 documented tools are listed |
| 2 | Confirm none of them is an "edit sent message" / "update message" action | No such tool exists in the list |
| 3 | Ask the agent in chat to "edit the email I already sent" | Agent reports it has no capability to do this, rather than attempting an unsupported Graph call |

## Expected Final State

No edit-sent-message tool exists anywhere in the toolkit's tool set.

## Pass/Fail Criteria

**Pass:**
- No such tool appears in the tool list
- Agent correctly reports the limitation instead of attempting the action

**Fail:**
- A tool purporting to edit a sent message exists or is callable
