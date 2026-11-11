---
id: ELITEA-4674
title: "Balanced and Full Window Budget Math Is Correct for Small and Large Context Windows"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Access to at least one model with a 128,000-token context window and one model with a context window > 272,000 tokens

## Test Data

| Field | Value |
|-------|-------|
| Small-window model | ~128,000 token context window |
| Large-window model | 1,000,000 token context window (AC6's worked example model) |
| Expected Safety margin (128k) | 1,280 (1% of 128,000) |
| Expected Minimum output allowance | 1,024 (Auto) |
| Expected available window (128k) | ≈ 126,720 |
| Expected Total window, Balanced (1M model) | 272,000 (capped) |
| Expected available window, Balanced (1M model) | 269,280 (272,000 − 1% safety margin of 2,720) |
| Expected Total window, Full (1M model) | 1,000,000 |
| Expected available window, Full (1M model) | 990,000 (1,000,000 − 1% safety margin of 10,000) |
| Expected summarization floor, Full (1M model) | No summarization below ~890,000 tokens of usage (90% of usable_input ≈ 988,976 − 1,024 reserved output) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat on the 128,000-token model in Balanced mode. Open the Context management card. | Total window = 128,000; Safety margin = 1,280; Minimum output allowance = 1,024 (Auto); available window ≈ 126,720. |
| 2 | Switch this same chat to Full mode. | All values are identical to Balanced (since 128,000 ≤ 272,000); a hint is shown that Balanced and Full are equivalent for this model. |
| 3 | Open a chat on the 1,000,000-token model (AC6's example) in Balanced mode. Open the Context management card. | Total window = 272,000 (capped, not the model's full window); available window = 269,280 (272,000 minus the ~1% safety margin). |
| 4 | Switch the same chat to Full mode. | Total window = 1,000,000 (the model's actual full window); available window = 990,000 (1,000,000 minus the ~1% safety margin) — recalculated from the full value, not from 272,000. |
| 5 | With Full mode active and Automatic Summarization enabled, send messages and monitor cumulative usage approaching the summarization trigger. | Summarization does NOT fire while usage remains below ~890,000 tokens (i.e., below 90% of the ~988,976-token usable input in Full mode for this model). |

## Expected Final State

Budget numbers for both a small-window (128k) and the large-window (1M, AC6) model match the documented calculation rules in both Balanced and Full modes, including the exact AC6 worked-example figures (272,000/269,280 in Balanced; 1,000,000/990,000 in Full; no premature summarization below ~890k in Full).

## Pass/Fail Criteria

**Pass:**
- All numeric values (Total window, Safety margin, Minimum output allowance, available window) match the expected calculation for both models and both modes
- The "modes are identical" hint appears for the small-window model
- The 1M model's Balanced figures match 272,000 / 269,280 and its Full figures match 1,000,000 / 990,000 exactly, per AC6
- No summarization fires below ~890,000 tokens of usage in Full mode on the 1M model

**Fail:**
- Any displayed value deviates from the documented calculation
- Full mode for the large-window model still shows 272,000 instead of the model's true window
- The "identical modes" hint is missing for the small-window model, or incorrectly shown for the large-window model
- The 1M model's Balanced/Full figures do not match the AC6 worked example, or summarization fires prematurely below the ~890k floor
