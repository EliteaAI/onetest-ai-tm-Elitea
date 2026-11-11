---
id: ELITEA-4684
title: "Regression Revalidation of Legacy Max Context Tokens Based Test Cases Against New UI"
priority: high
type: regression
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Scope Note

One-time audit/deprecation task for stale pre-existing test cases, not a reusable recurring check — not added to the standing regression suite. Run once to close out the migration, then retire.

## Preconditions

- User is logged in to `{{base_url}}`
- Access to the OneTest repository to cross-reference ELITEA-3744, ELITEA-2376, ELITEA-2390, ELITEA-2391, ELITEA-2374, ELITEA-3795, and ELITEA-3790

## Test Data

| Field | Value |
|-------|-------|
| Stale test cases reviewed | ELITEA-3744, ELITEA-2376, ELITEA-2390, ELITEA-2391, ELITEA-2374, ELITEA-3795, ELITEA-3790 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attempt to execute ELITEA-3744 (Context Budget Panel Reflects Profile Max Context Tokens) as written. | Test cannot pass as written because the Max Context Tokens profile field no longer exists; flag for deprecation/rewrite rather than logging a new product defect. |
| 2 | Attempt to execute ELITEA-2376 (Max Context Tokens and Preserve Recent Messages persist) and ELITEA-2390 (Context management settings apply to new conversations only). | Both reference the removed field by name and cannot pass as written; flag both for rewrite around `default_context_window_mode`. |
| 3 | Attempt to execute ELITEA-2391 (Max Context Tokens does not accept non-numeric or negative values). | The numeric input no longer exists; flag for deprecation since the validation no longer applies to a radio control. |
| 4 | Review ELITEA-2374 (Context management toggle enables/disables token fields). | Its steps already reference the Balanced/Full radio, but its title/objective still mention "token fields"; flag for a title/objective correction only (not a functional defect). |
| 5 | Attempt ELITEA-3795 (Context management functions in Bare mode). | The "Max Context Tokens: 1000" precondition can no longer be configured; flag for rewrite using Balanced/Full plus a small-window model to force quick summarization. |
| 6 | Open the Context Management modal with "Bare" personality active and review against ELITEA-3790 (Bare option appears in modal persona dropdown). | The new Context window section now appears above Persona Management in the modal; confirm this addition does not break the Persona Management section or hide the "Bare" option in the dropdown. |

## Expected Final State

All listed stale test cases are confirmed as needing deprecation/rewrite (items 1–5) or a documentation-only correction (item 4), and the modal layout change is confirmed not to regress the Bare-mode persona dropdown (item 6).

## Pass/Fail Criteria

**Pass:**
- Each stale test case's failure mode matches the expected "field removed" reason, not an unrelated defect
- ELITEA-3790's "Bare" option is still visible and selectable despite the modal's new Context window section

**Fail:**
- A stale test case fails for a reason unrelated to the removed field (indicating a separate, real regression)
- The "Bare" option is missing, hidden, or broken by the modal's new layout
