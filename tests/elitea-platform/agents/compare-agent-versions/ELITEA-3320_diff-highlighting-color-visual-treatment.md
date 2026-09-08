---
id: ELITEA-3320
title: "Diff highlighting displays with color and visual treatment for changed Agent content"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2 versions containing different Instructions content

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version 1 Instructions | "You are a helpful AI assistant. Always be polite." |
| Version 2 Instructions | "You are a helpful AI assistant. Always be professional and polite." |
| Change Type Added | "Always be professional and" (added text) |
| Change Type Removed | N/A in this scenario |
| Change Type Modified | "polite" remains in both |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Navigate to Instructions section | Instructions text displayed for both versions |
| 3 | Verify changed lines/text are highlighted with color | Added text "Always be professional and" is highlighted (e.g., green/yellow background) |
| 4 | Verify highlighting includes **additional visual treatment** beyond color | Highlighting uses pattern, border, icon, or other visual indicator in addition to color |
| 5 | Verify unchanged content is NOT highlighted | Unchanged text "You are a helpful AI assistant. Always be polite." has no highlighting |
| 6 | Test with text removed scenario: create new versions where text is deleted | Removed text is highlighted with different color/treatment (e.g., red) |
| 7 | Switch to dark theme in user settings | Theme changes to dark mode |
| 8 | Reopen Compare Versions modal | Modal opens in dark theme |
| 9 | Verify highlighting is visible and readable in dark theme | Diff colors/patterns are visible and contrast properly with dark background |
| 10 | Verify screen reader accessible descriptions exist for differences | ARIA labels or accessible text describe "added content" or "removed content" |

## Expected Final State

Diff highlighting is visible with both color and additional visual treatment, works in light and dark themes, and provides accessible descriptions for highlighted differences.

## Pass/Fail Criteria

**Pass:**
- Changed content is highlighted with color
- Additional visual treatment is present (not color alone)
- Unchanged content has no highlighting
- Highlighting visible in both light and dark themes
- Accessible descriptions provided

**Fail:**
- No highlighting visible for changes
- Only color used (no additional visual treatment)
- Unchanged content is highlighted incorrectly
- Highlighting not visible in dark theme
- No accessibility support for differences
