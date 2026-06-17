---
id: ELITEA-0386
title: "Not Published Agent in Chat — Edit LLM Settings After Version Switch — No Spurious Error"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [eng:frontend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4941]
---
# ELITEA-0386: Not Published Agent in Chat — Edit LLM Settings After Version Switch — No Spurious Error

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that editing LLM settings for a non-published agent in Chat after switching the agent version does not produce a spurious "LLM settings override is only allowed for published agents from agent studio" error alongside the success message.

**Coverage:**
- Non-published agent added to Chat; agent version switched to a different version
- LLM settings edited WITHOUT a page reload after the version switch
- Only a success notification is shown on save — no simultaneous LLM override error
- Error is reproduced consistently after each version switch (not a one-time fluke)
- Parametrized LLM setting changes: LLM model, temperature/creativity, token limit, reasoning settings

## Preconditions

- Logged in to {{base_url}}
- A non-published agent is available in the project with at least 2 saved versions (e.g., "base" and one additional version)
- Browser: Chrome or Firefox, latest stable
- A new chat session is open (no prior page reload between steps)

## Test Data

**Agent:** Any non-published agent with at least 2 versions available in the version selector

**LLM setting changes to test (parametrized — repeat for each):**

| Variant | Setting | Change |
|---------|---------|--------|
| A | LLM model | Switch to any different available model |
| B | Temperature / Model creativity | Adjust slider by any value (e.g. 0.6 → 0.8) |
| C | Token limit | Change max_tokens (e.g. -1 → 2048) |
| D | Reasoning settings | Toggle or change reasoning effort level |

**Chat:** New chat created in the current session — do NOT reload at any point during the test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a project and create a new Chat session. | Empty chat opens with no participants. |
| 2 | Add the non-published agent to the chat. | Agent is added as a participant. The agent version selector is visible in the chat. |
| 3 | In the agent version selector, switch to a different version (e.g. from 'base' to version 2). | Version switches successfully. A success notification may appear. The page is NOT reloaded. |
| 4 | WITHOUT reloading the page, open the LLM settings panel for the agent in the chat. | LLM settings panel opens showing current model, temperature, token limit, and reasoning settings. |
| 5 | Modify any LLM setting (Variant A: change LLM model to any other available model). | New model is selected in the UI. |
| 6 | Save the LLM settings change. Observe all toast notifications that appear. | Only a success notification appears. The error 'LLM settings override is only allowed for published agents from agent studio' does NOT appear. |
| 7 | Switch the agent version again (e.g. back to 'base'). Then immediately modify a different LLM setting (Variant B: adjust temperature). Save. | Only a success notification appears. The spurious LLM override error does NOT appear after a second version switch either. |
| 8 | Repeat the version switch → LLM edit → save cycle for Variants C (token limit) and D (reasoning settings). | No spurious LLM override error appears for any LLM setting variant after any version switch. Only success notifications are shown each time. |

## Expected Final State

No spurious LLM override error appears for any LLM setting variant after any version switch. Only success notifications are shown each time.

## Pass/Fail Criteria

**Pass:**
- After every agent version switch, editing and saving any LLM setting shows only a success notification
- The error "LLM settings override is only allowed for published agents from agent studio" never appears for a non-published agent
- The issue does not appear after the first switch only — it is confirmed absent after repeated version switches

**Fail:**
- After switching the agent version, saving any LLM setting triggers the spurious "LLM settings override" error alongside (or instead of) the success message
- The error disappears only after a page reload, confirming the frontend state is corrupted by the version switch
