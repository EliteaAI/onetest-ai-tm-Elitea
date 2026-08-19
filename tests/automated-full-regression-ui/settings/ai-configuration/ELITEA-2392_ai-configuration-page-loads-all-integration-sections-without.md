---
id: ELITEA-2392
title: "AI Configuration page loads all integration sections without error"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_ai_providers_page_sections_load_without_error.TestAIProvidersPageSections.test_ai_providers_page_sections_load_without_error_test
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1252
---

# ELITEA-2392: AI Configuration page loads all integration sections without error

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that AI Configuration page loads all integration sections without error. Success is confirmed when verify the "ai configuration" and "openai template" tabs are present at the top.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → AI Configuration | Target page/section loads successfully. |
| 2 | Verify the page loads without error or blank state | Condition holds as described. |
| 3 | Verify the following sections are visible in order: | Condition holds as described. |
| 4 | LLM Models (with Default / High-tier / Low-tier selectors) | Action completes without error and produces the expected UI state. |
| 5 | Embedding Models (with Default embedding model selector) | Action completes without error and produces the expected UI state. |
| 6 | Vector Storage (with Default vector storage selector) | Action completes without error and produces the expected UI state. |
| 7 | Image Generation (with Default image generation model selector) | Action completes without error and produces the expected UI state. |
| 8 | Speech Recognition / ASR (with Default ASR model selector) | Action completes without error and produces the expected UI state. |
| 9 | Text to Speech / TTS (with Default TTS model selector) | Action completes without error and produces the expected UI state. |
| 10 | AI credentials (if configured) | Action completes without error and produces the expected UI state. |
| 11 | Verify each section contains at least one configuration card | Condition holds as described. |
| 12 | Verify the "AI Configuration" and "OpenAI Template" tabs are present at the top | Condition holds as described. |

---

## Expected Final State

Verify the "AI Configuration" and "OpenAI Template" tabs are present at the top.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: AI Configuration page loads all integration sections without error.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
