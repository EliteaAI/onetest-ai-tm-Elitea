---
id: ELITEA-0557
title: "Chipset Format Is Consistent Across Chat, Agent, and Pipeline Contexts"
priority: high
type: functional
module: chipset-display
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0557: Chipset Format Is Consistent Across Chat, Agent, and Pipeline Contexts

**Module:** Chipset Display · **Priority:** High · **Type:** Functional

**Objective:** Verify chipset naming format is identical for the same entity type regardless of whether it executes in Chat, Agent, or Pipeline context.

**Coverage:**
- LLM chipset format (icon + display name) is identical across Chat, Agent, and Pipeline execution traces
- Toolkit chipset format (icon + user-defined name + action) is identical across all three contexts
- No context-specific naming variation or icon difference exists for the same entity

## Preconditions

- Logged in to ELITEA at {{base_url}}
- The same LLM model is configured in: (a) a Chat conversation, (b) a target Agent, (c) a target Pipeline step
- The same Toolkit (e.g., myJiraTracker) is configured in both the Agent and Pipeline
- All three contexts are able to invoke the LLM and Toolkit
- Browser: Chrome/Edge latest

## Test Data

- Same LLM configured across Chat, Agent, Pipeline (e.g., GPT-4o Mini)
- Same Toolkit configured in Agent and Pipeline (e.g., myJiraTracker)
- Test prompt: "Summarize this and create a Jira ticket"
- Contexts: Chat conversation, Agent chat tab, Pipeline History Runs
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Confirm that the target LLM model and target Toolkit are configured in: (a) the Chat LLM assignment, (b) the target Agent, and (c) the target Pipeline step. | All three contexts share the same LLM and Toolkit. |
| 2 | [Chat context] Navigate to Chat via the left sidebar. Open the target conversation (or start a new one). Send a prompt that triggers both the LLM and the Toolkit (e.g., 'Summarize this and create a Jira ticket'). Press Send. | Chat processes the prompt; both LLM and Toolkit are invoked; execution trace becomes visible. |
| 3 | Open the execution trace in Chat. Locate the LLM chipset. Record the exact icon appearance and label text (e.g., label = 'GPT-4o Mini'). | LLM chipset label and icon noted. |
| 4 | In the same Chat trace, locate the Toolkit chipset. Record its exact icon and label text (e.g., 'myJiraTracker: createIssue'). | Toolkit chipset label and icon noted. |
| 5 | [Agent context] Navigate to Agents via the left sidebar. Open the target agent. Switch to the Chat tab. Send the same prompt as step 2. Wait for completion. | Agent processes the prompt; LLM and Toolkit are invoked. |
| 6 | Open the execution trace in the Agent. Locate the LLM chipset. Compare its icon and label text to what was recorded in step 3. | Icon and label are identical to the Chat context — same icon style, same display name text. |
| 7 | In the Agent execution trace, locate the Toolkit chipset. Compare its icon and label to what was recorded in step 4. | Icon and label are identical to the Chat context chipset. |
| 8 | [Pipeline context] Navigate to Pipelines via the left sidebar. Open the target pipeline containing the LLM step and Toolkit step. Click Run and wait for completion. | Pipeline executes and completes. |
| 9 | Go to the pipeline's History Runs tab. Open the completed run. Locate the LLM chipset. Compare its icon and label to steps 3 and 6. | LLM chipset icon and label are identical across all three contexts (Chat, Agent, Pipeline). |
| 10 | Locate the Toolkit chipset in the Pipeline run. Compare its icon and label to steps 4 and 7. | Toolkit chipset icon and label are identical across all three contexts — zero differences in naming convention, icon style, or structure. |

## Expected Final State

Toolkit chipset icon and label are identical across all three contexts — zero differences in naming convention, icon style, or structure.

## Pass/Fail Criteria

**Pass:**
- LLM chipset icon and label text are identical in Chat, Agent, and Pipeline traces
- Toolkit chipset icon and label text are identical in Chat, Agent, and Pipeline traces
- Zero differences in naming convention, icon style, or structure across any context

**Fail:**
- Any context shows a different chipset label or icon for the same entity
- Chat trace uses different format than Agent or Pipeline trace
