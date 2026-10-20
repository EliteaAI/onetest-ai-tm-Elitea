---
id: ELITEA-4120
title: "Verify show-more control appears or is withheld based on line-overflow thresholds for welcome message and description"
priority: critical
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}` with permissions to create, edit, and publish agents
- Tester is aware truncation is driven by rendered line overflow (welcome message: 8-line clamp; description: 2-line clamp), not a fixed character count

## Test Data

| Field | Variant | Content guidance |
|-------|---------|-------------------|
| Welcome message | Not enough (fits within 8 lines) | Short text, no overflow |
| Welcome message | Enough (exceeds 8 lines) | Long text that wraps beyond 8 lines at default card width |
| Welcome message | Max-char limit | Text at exactly the editor's maximum allowed character count |
| Description | Not enough (fits within 2 lines) | Short text, fits within 2 lines |
| Description | Enough (exceeds 2 lines) | Long text that wraps beyond 2 lines |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create and publish 5 separate agents, one per Test Data row, entering the specified content in the corresponding field while keeping the other field short | All 5 agents publish successfully |
| 2 | Open Agents Studio | All 5 agent cards are visible |
| 3 | For the two "Not enough" variants, inspect the card | Full field text is shown; no "Show more" control appears |
| 4 | For the "Enough" and "Max-char limit" variants, inspect the card | Text is visually clamped (cut off); "Show more" control appears |
| 5 | Click "Show more" for each clamped variant | Full text is revealed |
| 6 | Compare each revealed text to what was entered in the editor, paying particular attention to the final characters for the Max-char limit variant | Text matches exactly with no missing or extra characters |

## Expected Final State

Each of the 5 cards shows line-clamp behavior consistent with its content length; clamped cards reveal complete, accurate text when expanded.

## Pass/Fail Criteria

**Pass:**
- "Not enough" variants never display "Show more"
- "Enough"/"Max-char limit" variants always display "Show more" and reveal the exact, complete saved text

**Fail:**
- "Show more" appears for content that fits within the clamp (false positive)
- "Show more" is missing for content that overflows the clamp (false negative)
- Expanded text does not match the saved text, especially at the character-limit boundary
