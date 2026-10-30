---
id: ELITEA-3825
title: "Skill — Run Settings (Model, Context, Execution)"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:run-settings, r-2.0.8, regression:merged]
requirements: []
---

# ELITEA-3825: Skill — Run Settings (Model, Context, Execution)

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify complete run_settings functionality for skills including configuring fixed model with reasoning level and max tokens, persistence after save and reload, test panel initialization with saved settings, execution using configured model (not project default), and context toggle excluding project context when disabled. Success is confirmed when all run_settings configurations work correctly and are applied during execution.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- Multiple models are available for selection (e.g., Claude Opus, Claude Sonnet, GPT-4).
- Project has a default model configured (different from the model selected for the skill).
- Project context is configured and available.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill Name | Run Settings Test Skill |
| Skill Description | Skill for testing run_settings configuration |
| Skill Instructions | Answer the user's question about the current date and time. If project context is available, mention any project-specific information. |
| Fixed Model Selection | Claude Opus (or different from project default) |
| Reasoning Level | high |
| Max Tokens | 2000 |
| Context Toggle | OFF (ignore_project_context = true) |
| Test Prompt 1 | What is today's date? |
| Test Prompt 2 (context test) | Tell me about the project context |

---

## Steps

### Part 1: Configure Fixed Model with Reasoning Level and Max Tokens

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill with Name "Run Settings Test Skill", Description "Skill for testing run_settings configuration", Instructions "Answer the user's question about the current date and time. If project context is available, mention any project-specific information." | Skill is created successfully |
| 2 | Open the skill "Run Settings Test Skill" | Skill editor page loads |
| 3 | Navigate to "Run Settings" or "Model Settings" section (if separate tab or expandable section) | Run Settings section is displayed |
| 4 | Select a fixed model: "Claude Opus" (or model different from project default) | Model is selected |
| 5 | Verify "Reasoning Level" dropdown/selector appears (for reasoning-capable models) | Reasoning Level selector is displayed |
| 6 | Select reasoning level: "high" | Reasoning level is selected |
| 7 | Verify "Max Tokens" input field appears | Max Tokens field is displayed |
| 8 | Enter max tokens: "2000" | Max tokens value is entered |
| 9 | Click Save | Skill is saved with run_settings configuration |

### Part 2: Persistence After Save and Reload

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Navigate away from the skill (e.g., return to Skills list) | Navigation completes successfully |
| 11 | Re-open the skill "Run Settings Test Skill" | Skill editor page loads |
| 12 | Navigate to "Run Settings" section | Run Settings section is displayed |
| 13 | Verify fixed model "Claude Opus" is still selected | Model persisted correctly |
| 14 | Verify reasoning level "high" is still selected | Reasoning level persisted correctly |
| 15 | Verify max tokens "2000" is still displayed | Max tokens persisted correctly |

### Part 3: Test Panel Initializes with Saved Settings

| # | Action | Expected Result |
|---|--------|-----------------|
| 16 | With the skill "Run Settings Test Skill" open, click "Test" or "Test Panel" button | Test panel opens |
| 17 | Verify the test panel displays the selected model: "Claude Opus" (not project default) | Test panel shows correct model |
| 18 | Verify reasoning level "high" is displayed or indicated in the test panel | Reasoning level is shown in test panel |
| 19 | Verify max tokens "2000" is displayed or indicated | Max tokens is shown in test panel |
| 20 | Verify the test panel uses these settings (not project defaults) | Test panel is initialized with skill's run_settings |

### Part 4: Skill Execution Uses Configured Model

| # | Action | Expected Result |
|---|--------|-----------------|
| 21 | In the test panel, enter prompt: "What is today's date?" | Prompt is entered |
| 22 | Click "Run" or "Send" to execute the skill | Skill execution starts |
| 23 | Verify the skill uses the configured model "Claude Opus" (check execution logs, thought process, or model indicator) | Execution uses "Claude Opus", not project default |
| 24 | Verify reasoning level "high" is applied (if visible in logs or execution metadata) | Reasoning level is applied |
| 25 | Verify max tokens "2000" is respected (response does not exceed 2000 tokens) | Max tokens limit is applied |
| 26 | Verify the skill responds correctly to the prompt | Skill executes successfully with configured settings |

### Part 5: Context Toggle OFF Excludes Project Context

| # | Action | Expected Result |
|---|--------|-----------------|
| 27 | Open the skill "Run Settings Test Skill" | Skill editor page loads |
| 28 | Navigate to "Run Settings" section | Run Settings section is displayed |
| 29 | Verify "Use Project Context" toggle or checkbox is present | Context toggle control is displayed |
| 30 | Set the "Use Project Context" toggle to OFF (or check "Ignore Project Context") | Context toggle is set to OFF (ignore_project_context = true) |
| 31 | Click Save | Skill is saved with context disabled |
| 32 | Open the test panel for the skill | Test panel opens |
| 33 | Enter prompt: "Tell me about the project context" | Prompt is entered |
| 34 | Click "Run" or "Send" to execute | Skill execution starts |
| 35 | Verify the response does NOT include project-specific context information | Project context is excluded from execution |
| 36 | (If possible) Inspect system prompt or execution logs and verify "ignore_project_context: true" is applied | Context exclusion is confirmed in execution metadata |
| 37 | Set the "Use Project Context" toggle back to ON | Context toggle is enabled |
| 38 | Save and execute again with the same prompt | Skill execution starts |
| 39 | Verify the response NOW includes project-specific context information (if available) | Project context is included when toggle is ON |

---

## Expected Final State

- Fixed model, reasoning level, and max tokens are configured and saved in run_settings
- All run_settings persist correctly after save, navigation, and reload
- Test panel initializes with the saved run_settings (not project defaults)
- Skill execution uses the configured model, reasoning level, and max tokens
- Context toggle OFF excludes project context from execution
- Context toggle ON includes project context in execution
- All run_settings are correctly applied during skill execution

---

## Pass/Fail Criteria

**Pass:**
- Fixed model "Claude Opus", reasoning level "high", and max tokens "2000" are saved and persist
- Test panel displays the saved run_settings correctly (not project defaults)
- Skill execution uses "Claude Opus" model (verified in logs/metadata)
- Reasoning level and max tokens are applied during execution
- Context toggle OFF excludes project context from execution
- Context toggle ON includes project context in execution
- All settings persist across save, navigation, and reload

**Fail:**
- Run_settings do not persist after save and reload
- Test panel initializes with project defaults instead of skill's run_settings
- Skill execution uses project default model instead of configured model
- Reasoning level or max tokens are not applied
- Context toggle OFF does not exclude project context
- Context toggle ON does not include project context
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-3825, ELITEA-3826, ELITEA-3827, ELITEA-3828

**Regression rationale:** Consolidated from 4 tests covering different aspects of run_settings: (1) ELITEA-3825 tests configuration persistence (fixed model, reasoning level, max tokens persist after reload), (2) ELITEA-3826 tests test panel initialization (initializes with saved settings), (3) ELITEA-3827 tests execution behavior (uses configured model during execution), and (4) ELITEA-3828 tests context control (context toggle OFF excludes project context). These tests cover the complete run_settings feature and can be merged into a single comprehensive test.

**Selected checkpoints:**
- Configure: fixed model "Claude Opus", reasoning "high", max tokens "2000"
- Persistence: save → reload → settings still present
- Test panel: initializes with saved settings (not project defaults)
- Execution: uses "Claude Opus" (not project default)
- Context OFF: project context excluded from execution
- Context ON: project context included in execution
