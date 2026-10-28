---
id: ELITEA-4184
title: "Verify UI updates correctly when switching between versions with different run_settings"
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
- Version 1 has run_settings: Model A, Reasoning Low, Context ON
- Version 2 has run_settings: Model B, Reasoning High, Context OFF

## Test Data

| Version | Model | Reasoning | Max Tokens | Context |
|---------|-------|-----------|------------|---------|
| v1 | GPT-4 Turbo | Low | 4096 | ON |
| v2 | Claude Opus | High | 8000 | OFF |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill details page | Skill page opens on default/latest version |
| 2 | Select Version 1 from version dropdown | Version 1 loaded |
| 3 | Expand "Run settings" accordion | Run settings section displays |
| 4 | Verify Model: GPT-4 Turbo | Model A displayed |
| 5 | Open Model settings → Verify Reasoning: Low, Max tokens: 4096 | Settings for v1 displayed |
| 6 | Verify "Include project context" toggle is ON | Context: ON |
| 7 | Close settings → Switch to Version 2 from dropdown | Version 2 loaded |
| 8 | Expand "Run settings" accordion (if collapsed) | Run settings section displays |
| 9 | Verify Model changed to: Claude Opus | Model B displayed |
| 10 | Open Model settings → Verify Reasoning: High, Max tokens: 8000 | Settings for v2 displayed |
| 11 | Verify "Include project context" toggle is OFF | Context: OFF |
| 12 | Switch back to Version 1 | Version 1 loaded again |
| 13 | Verify run_settings reverted to v1 configuration (Model A, Low, 4096, ON) | UI updates correctly |

## Expected Final State

- UI dynamically updates when switching versions
- Each version's run_settings display correctly
- No cross-contamination between versions
- Version switching is seamless

## Pass/Fail Criteria

**Pass:**
- Each version displays its own run_settings
- UI updates immediately on version change
- All fields (model, reasoning, tokens, context) update correctly
- No stale data displayed

**Fail:**
- UI does not update when switching versions
- Run_settings from one version persist when switching to another
- Partial update (some fields update, others don't)
- UI requires page reload to show correct settings
