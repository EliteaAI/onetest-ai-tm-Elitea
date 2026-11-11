---
id: ELITEA-4670
title: "GitHub Toolkit — Agent triggers a workflow, finds the new run and reports the failed step without a manual run ID"
priority: high
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4670: GitHub Toolkit — Agent triggers a workflow, finds the new run and reports the failed step without a manual run ID

**Module:** Github Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify the main use case of #2407 end to end in chat: an agent triggers a workflow, gets the new run ID with `get_workflow_runs`, checks its status and reads the failed step's logs, and the user never types a run ID.

**Coverage:**
- `trigger_workflow` → `get_workflow_runs` → `get_workflow_status` → `get_workflow_logs` in one conversation
- Run ID found by the agent, not entered by the user

## Preconditions
- Logged in to `{{base_url}}` as a project member
- An agent with a GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `trigger_workflow`, `get_workflow_runs`, `get_workflow_status` and `get_workflow_logs` turned on
- Workflow `runs-test-data.yml` takes input `outcome` (`success`, `failure` or `slow`). With `failure`, job `test` fails at step "Fail on purpose"

## Test Data
| Field | Value |
|-------|-------|
| Prompt 1 | Trigger the workflow runs-test-data.yml on main with input outcome = failure. |
| Prompt 2 | Find the run you just started and tell me its run ID and status. |
| Prompt 3 | When it finishes, show me which step failed and the log of the failed job only. |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a new chat with the agent and send Prompt 1. | The agent calls `trigger_workflow` with `outcome: failure` on `main` and confirms that it was triggered. |
| 2 | Send Prompt 2. | The agent calls `get_workflow_runs` for `runs-test-data.yml` and gives a run ID that is the newest run on the repo's GitHub Actions page. |
| 3 | Wait until the run finishes on GitHub (about 1 minute), then send Prompt 3. | The agent calls `get_workflow_status` and `get_workflow_logs` with `failed_only: true`, using the run ID from step 2. |
| 4 | Check the agent's answer to Prompt 3. | It says the run failed in job `test` at step "Fail on purpose" and shows log text containing `exit code 1`. |
| 5 | Review the whole conversation. | The user never typed a run ID. Every run ID came from a tool result. |

## Expected Final State
One new failed run of `runs-test-data.yml` exists, and the agent found and diagnosed it with no run ID from the user.

## Pass/Fail Criteria

**Pass:**
- All four tools succeed in one conversation, and the agent reports the correct run ID, result and failed step

**Fail:**
- The agent asks the user for a run ID, uses a wrong run ID, or any tool call fails
