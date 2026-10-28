---
id: ELITEA-4198
title: "Verify compare versions highlights difference in max tokens setting"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill with at least 2 versions exists
- Version 1 has max_tokens: 4096
- Version 2 has max_tokens: 8000
- Other settings (model, reasoning, context) are identical

## Test Data

| Version | Model | Reasoning | Max Tokens | Context |
|---------|-------|-----------|------------|---------|
| v1 | Claude Opus | Medium | 4096 | ON |
| v2 | Claude Opus | Medium | 8000 | ON |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill details page | Skill page opens |
| 2 | Click "Compare Versions" | Version comparison interface opens |
| 3 | Select Version 1 and Version 2 | Versions selected |
| 4 | Click "Compare" | Comparison view displays |
| 5 | Navigate to "Run settings" step in comparison | Run settings section visible |
| 6 | Observe Model field → Verify "No change" | Model: No change |
| 7 | Observe Reasoning level → Verify "No change" | Reasoning: No change |
| 8 | Observe Max tokens field → Verify shows difference: 4096 → 8000 (highlighted) | Max tokens: 4096 → 8000 (highlighted) |
| 9 | Observe Context toggle → Verify "No change" | Context: No change |
| 10 | Verify Max tokens difference is clearly visible with visual indicator (color, bold, arrow) | Max tokens change highlighted |

## Expected Final State

- Max tokens difference clearly displayed
- Only Max tokens field highlighted (other fields unchanged)
- Comparison format: 4096 → 8000 or similar
- Visual indicator (color, arrow) shows the change

## Pass/Fail Criteria

**Pass:**
- Max tokens difference (4096 → 8000) is highlighted
- Highlight is visually distinct
- Unchanged fields not highlighted
- Comparison is accurate

**Fail:**
- Max tokens difference not shown
- No highlighting on changed field
- All fields highlighted (false positive)
- Comparison incorrect or missing
