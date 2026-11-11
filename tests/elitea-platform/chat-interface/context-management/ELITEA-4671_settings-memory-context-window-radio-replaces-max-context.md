---
id: ELITEA-4671
title: "Settings Memory Context Window Radio Replaces Max Context Tokens Field"
priority: critical
type: functional
module: settings-memory
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## AC Update Note (ticket re-check, 2026-11-11)

Issue #6898's **AC4** was struck through on the ticket with the note "togle was deleted" — the Context Management on/off toggle no longer exists in the shipped UI. This case is corrected accordingly: the old steps/criteria about toggling Context Management off and back on are **removed** and replaced with a check that no such toggle exists at all. **AC1** is unaffected and still fully covered (radio group, descriptions, field removal, helper/summary copy).

## Preconditions

- User is logged in to `{{base_url}}`
- Settings → Memory is accessible for the current project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/memory` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Memory → Context Management section. | Section loads with no errors. |
| 2 | Inspect the controls shown directly under "Context Management". | A "Context window" radio group is present with exactly two options: "Balanced" (description mentions up to 272,000 tokens) and "Full" (description mentions the model's entire context window). |
| 3 | Search the entire page for any numeric "Max Context Tokens" input. | No such field exists anywhere on the page. |
| 4 | Inspect the layout below the radio group. | "Preserve Recent Messages" is shown as its own full-width field below the Context window radio group (not combined with the old token field). |
| 5 | Search the entire page for a "Context Management" on/off toggle control. | No such toggle exists anywhere on the page (removed per AC4) — the Context window radio group and Automatic Summarization area always visible|
| 6 | Inspect the helper text directly below the Context window radio group. | Helper text reads (or matches in substance): "Output and a safety margin are reserved inside the window. When automatic summarization is enabled, compaction starts at 90% of usable input." |
| 7 | Inspect the Automatic Summarization section's description text. | Description reads (or matches in substance): "Compact older history at 90% of usable input, retaining recent messages and authoritative instructions." (not the old 64,000-token-based copy). |

## Expected Final State

Settings → Memory shows only the new Context window radio (Balanced/Full) with no legacy numeric Max Context Tokens field and no Context Management on/off toggle (removed per AC4), and the helper/description copy under both sections reflects the new 90%-of-usable-input compaction model (AC1).

## Pass/Fail Criteria

**Pass:**
- Context window radio group with Balanced and Full options is present and correctly described
- No "Max Context Tokens" numeric field is present anywhere on the page
- Preserve Recent Messages is its own field, independent of the radio group
- No "Context Management" on/off toggle control exists anywhere on the page
- The Context window helper text and the Automatic Summarization description both match the new 90%-of-usable-input copy specified in AC1

**Fail:**
- A numeric "Max Context Tokens" field is still present
- The Balanced/Full radio group is missing, mislabeled, or shows incorrect descriptions
- A "Context Management" on/off toggle control is still present anywhere on the page
- The helper text or Automatic Summarization description still references the old 64,000-token model or is missing/incorrect
