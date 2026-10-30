---
id: ELITEA-4222
title: "Re-validate toolkit Test Settings flows for existing tools after start screen change"
priority: high
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4222: Re-validate toolkit Test Settings flows for existing tools after start screen change

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkits exist: Artifact (with a bucket containing a text file), Remote MCP, ADO Repos (with a known pull request ID)
- A toolkit exists that uses a credential the current user can't access

## Test Data

| Field | Value |
|-------|-------|
| Artifact tools | `createFile`, `read_file` |
| Remote MCP tool | Any tool of the MCP server |
| ADO tool | `get_pull_request`, PR ID of an existing pull request |
| Long-output tool | Artifact `read_file` on a file with 200+ lines |
| Related cases | ELITEA-1127, ELITEA-0348, ELITEA-1937, ELITEA-1149, ELITEA-1194, ELITEA-0519 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Artifact toolkit → **Test** → pick `createFile`. Fill in the form, switch to `read_file` and back to `createFile`. | The `createFile` form is reset to its defaults (ELITEA-1127). |
| 2 | On the Artifact toolkit Test page, pick `read_file`. | The extra parameter fields are shown (ELITEA-0348). |
| 3 | Open the Remote MCP toolkit → **Test** → pick a tool and run it. | The tool runs and returns a result; if the MCP needs auth, the auth modal appears (ELITEA-1937). |
| 4 | Open the ADO Repos toolkit → **Test** → pick `get_pull_request`, enter the PR ID and run it. | The pull request details are returned (ELITEA-1149). |
| 5 | Open the toolkit with the inaccessible credential → **Test**. | Tools are listed or blocked with an explanation (ELITEA-1194). |
| 6 | Run Artifact `read_file` on the 200+ line file. | The output is shown and the results scrollbar is visible and works (ELITEA-0519). |

## Expected Final State

Existing Test Settings flows work the same way after picking tools from the new start screen.

## Pass/Fail Criteria

**Pass:**
- All six flows behave as in the related existing test cases

**Fail:**
- Any flow breaks, shows a wrong form, or behaves differently from its related test case
