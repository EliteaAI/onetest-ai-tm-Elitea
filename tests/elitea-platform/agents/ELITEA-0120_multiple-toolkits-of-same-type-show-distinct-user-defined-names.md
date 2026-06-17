---
id: ELITEA-0120
title: "Multiple Toolkits of Same Type Show Distinct User-Defined Names"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0120: Multiple Toolkits of Same Type Show Distinct User-Defined Names

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when an agent uses two toolkits of the same type, each chipset shows its distinct user-defined name — making it immediately clear which toolkit instance was used.

**Coverage:**
- Two same-type toolkits (both Jira) produce chipsets with distinct user-defined names
- "Project Alpha Jira: createIssue" and "Project Beta Jira: createIssue" are clearly distinguishable
- No generic names (e.g., "Jira: createIssue") replace user-defined names
- User can identify which Jira instance was used from the chipset alone

## Preconditions

- Logged in to ELITEA at {{base_url}}
- Two Jira-type toolkits configured with distinct user-defined names: "Project Alpha Jira" and "Project Beta Jira"
- Both toolkits added to the same Agent
- Agent prompt can trigger tool calls from both Jira toolkits
- Browser: Chrome/Edge latest

## Test Data

- Toolkit 1: "Project Alpha Jira" (Jira type), tool: createIssue
- Toolkit 2: "Project Beta Jira" (Jira type), tool: createIssue
- Both added to same Agent
- Test prompt: "Create a bug issue for Project Alpha and a task issue for Project Beta"
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Navigate to Agents and open the target agent. In the agent's Settings / Toolkits section, verify that both Project Alpha Jira and Project Beta Jira are listed, each with their exact user-defined name. | Both toolkits are confirmed with their distinct names in the agent's configuration. |
| 2 | Switch to the agent's Chat or Run tab. Enter a prompt that requires creating an issue in each Jira project (e.g., 'Create a bug issue for Project Alpha and a task issue for Project Beta'). Press Send. | Agent processes the prompt and invokes tool calls from both Jira toolkits. |
| 3 | Wait for execution to complete. Open the thinking steps / execution trace panel. | Execution trace shows multiple chipsets including entries for both Jira toolkit calls. |
| 4 | Locate the chipset for the Project Alpha Jira tool call. Read the full label. | Chipset label reads 'Project Alpha Jira: createIssue' — exact user-configured name; no generic label like 'Jira: createIssue'. |
| 5 | Locate the chipset for the Project Beta Jira tool call. Read the full label. | Chipset label reads 'Project Beta Jira: createIssue' — distinct from the Alpha chipset; exact user-configured name preserved. |
| 6 | Compare the two chipset labels side by side. Verify a user can immediately and unambiguously identify which Jira instance each call belongs to without any additional context. | The two chipsets are visually distinct with unique names — no ambiguity about which Jira instance was used. |

## Expected Final State

The two chipsets are visually distinct with unique names — no ambiguity about which Jira instance was used.

## Pass/Fail Criteria

**Pass:**
- Chipset for first toolkit reads "Project Alpha Jira: createIssue" — exact user-defined name
- Chipset for second toolkit reads "Project Beta Jira: createIssue" — distinct from the first
- User can identify each Jira instance without any additional context

**Fail:**
- Both chipsets show the same label (e.g., "Jira: createIssue") — instances are indistinguishable
- Either chipset uses a system-generated rather than user-defined name
