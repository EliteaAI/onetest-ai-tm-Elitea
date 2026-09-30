---
id: ELITEA-3518
title: "Toolkit Reuses the Credential's Existing Token Without a Second Login"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3518: Toolkit Reuses the Credential's Existing Token Without a Second Login

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that once its linked credential is authorized, the toolkit itself does not require any separate OAuth login step to become usable — the token lookup key matches between credential and toolkit flows.

## Preconditions

- An Outlook credential authorized per ELITEA-3504
- Toolkit created per ELITEA-3517 using that credential

## Test Data

- Existing `outlook-toolkit-e2e` toolkit linked to an authorized credential

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the `outlook-toolkit-e2e` toolkit | No "Login"/"Authorize" control is shown on the toolkit itself |
| 2 | Assign the toolkit to an agent and invoke a tool (e.g. `list_messages`) from agent chat | Tool executes successfully using the credential's existing token — no OAuth prompt appears |

## Expected Final State

The toolkit executes tools immediately using the linked credential's token, with no additional authorization step.

## Pass/Fail Criteria

**Pass:**
- Toolkit has no independent login control
- First tool invocation succeeds without any new OAuth prompt

**Fail:**
- Toolkit exposes/requires its own separate login
- Tool invocation triggers an unexpected OAuth prompt despite the credential already being authorized
