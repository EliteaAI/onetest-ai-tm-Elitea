---
id: ELITEA-4197
title: "Verify compare versions highlights differences in reasoning levels and displays Run settings step"
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
- Version 1 has run_settings: Model A, Reasoning Low, Max tokens 4096, Context ON
- Version 2 has run_settings: Model A, Reasoning High, Max tokens 4096, Context ON
- User has permission to compare versions

## Test Data

| Version | Model | Reasoning | Max Tokens | Context |
|---------|-------|-----------|------------|---------|
| v1 | GPT-4 Turbo | Low | 4096 | ON |
| v2 | GPT-4 Turbo | High | 4096 | ON |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill details page | Skill page opens |
| 2 | Click "Compare Versions" or similar action | Version comparison interface opens |
| 3 | Select Version 1 and Version 2 for comparison | Versions selected |
| 4 | Click "Compare" | Comparison view displays |
| 5 | Verify "Run settings" step/section appears in comparison | Run settings section visible |
| 6 | Observe Model field → Verify shows "No change" (both use GPT-4 Turbo) | Model: No change |
| 7 | Observe Reasoning level → Verify shows difference: Low → High (highlighted) | Reasoning: Low → High (highlighted/colored) |
| 8 | Observe Max tokens → Verify shows "No change" (both 4096) | Max tokens: No change |
| 9 | Observe Context toggle → Verify shows "No change" (both ON) | Context: No change |
| 10 | Verify only changed fields are highlighted or marked | Only Reasoning field highlighted |

## Expected Final State

- Compare Versions includes "Run settings" step
- Differences in run_settings are clearly highlighted
- Unchanged fields show "No change" or are not highlighted
- User can easily identify what changed between versions

## Pass/Fail Criteria

**Pass:**
- Run settings comparison section exists
- Reasoning difference (Low → High) is highlighted
- Unchanged fields (Model, Max tokens, Context) show no change
- Comparison is clear and accurate

**Fail:**
- No Run settings section in comparison
- Differences not highlighted
- All fields highlighted even if unchanged
- Comparison missing or incorrect
