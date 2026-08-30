---
id: ELITEA-2406
title: "TTS section displays model cards and default selector"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_ai_provider_section_cards_and_default_selector.TestAiProviderSectionCardsAndDefaultSelector.test_section_shows_model_cards_and_default_selector[ELITEA-2406-tts]
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1995"
---

# ELITEA-2406: TTS section displays model cards and default selector

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that TTS section displays model cards and default selector. Success is confirmed when click the selector — verify a dropdown of available tts models appears.

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
| 2 | Locate the Text to Speech (TTS) section | Action completes without error and produces the expected UI state. |
| 3 | Verify at least one model card is shown with: model name and status badge | Condition holds as described. |
| 4 | Verify the "Default TTS model" selector shows a non-empty value | Condition holds as described. |
| 5 | Click the selector — verify a dropdown of available TTS models appears | Control responds; expected next state is shown. |

---

## Expected Final State

Click the selector — verify a dropdown of available TTS models appears.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: TTS section displays model cards and default selector.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
