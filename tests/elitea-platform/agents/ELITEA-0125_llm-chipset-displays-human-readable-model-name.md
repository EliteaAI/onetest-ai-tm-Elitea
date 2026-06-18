---
id: ELITEA-0125
title: "LLM Chipset Displays Human-Readable Model Name"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0125: LLM Chipset Displays Human-Readable Model Name

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that LLM execution steps show the user-friendly model display name and never the raw technical model ID.

**Coverage:**
- LLM chipset shows display name, not technical ID (e.g., shows "GPT-4o Mini" not "gpt-4o-mini")
- No versioned suffix visible (e.g., no "gpt-4o-mini-2024-07-18")
- Chipset updates to reflect new model display name after model switch
- Applies in Agent chat execution context

## Preconditions

- Logged in to ELITEA at {{base_url}}
- An Agent exists configured with an LLM whose technical model ID is known (e.g., gpt-4o-mini, claude-sonnet-4-6)
- User has access to the agent's execution trace panel
- Browser: Chrome/Edge latest

## Test Data

- Agent LLM model 1: gpt-4o-mini (expected display name: GPT-4o Mini)
- Agent LLM model 2: claude-sonnet-4-6 (expected display name: Claude 4.6 Sonnet)
- Test prompt: "Hello"
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA at {{base_url}} In the left sidebar, click Agents. | The Agents list page loads. |
| 2 | Locate and open an Agent configured with an LLM whose technical model ID is known (e.g., gpt-4o-mini). Open the agent's Settings / Configuration tab and note the exact technical model ID shown there. | Agent configuration page loads; technical model ID is visible in settings (e.g., gpt-4o-mini). |
| 3 | Click the Run button or switch to the Chat tab within the agent. | Chat input is ready to accept a prompt. |
| 4 | Type any short prompt (e.g., Hello) and press Send. | Agent sends the message and begins processing. |
| 5 | Wait for the response to complete. Locate the thinking steps / execution trace panel that appears alongside or below the response. | Execution trace panel is visible with at least one chipset entry. |
| 6 | In the execution trace, find the chipset corresponding to the LLM step. Read the chipset label character by character. | Chipset is present with an LLM icon and a text label. |
| 7 | Verify the chipset label shows the human-readable display name (e.g., GPT-4o Mini) and does NOT contain the raw technical ID (gpt-4o-mini) or any versioned suffix (e.g., gpt-4o-mini-2024-07-18). | Chipset label shows display name only — no raw ID or version string visible. |
| 8 | Return to the Agent settings and switch the LLM model to a different one (e.g., claude-sonnet-4-6). Save the configuration. | Model change is saved successfully. |
| 9 | Re-run the agent with the same prompt. In the new execution trace, locate the LLM chipset and verify it shows the updated display name (e.g., Claude 4.6 Sonnet) — not the technical string claude-sonnet-4-6. | New LLM chipset shows updated display name without a raw model ID. |

## Expected Final State

New LLM chipset shows updated display name without a raw model ID.

## Pass/Fail Criteria

**Pass:**
- All LLM chipsets show human-readable display names with appropriate icon
- No versioned suffix or raw model ID string is visible in any chipset
- Chipset updates correctly when model is changed

**Fail:**
- Any chipset shows a raw technical model ID (e.g., gpt-4o-mini)
- Any chipset shows a versioned ID suffix (e.g., gpt-4o-mini-2024-07-18)
- Chipset does not update after model change
