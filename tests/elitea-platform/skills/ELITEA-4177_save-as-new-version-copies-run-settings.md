---
id: ELITEA-4177
title: "Verify 'Save as new version' copies run settings to the new version"
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
- A skill with configured run_settings already exists (fixed model, reasoning level, max tokens, context toggle)

## Test Data

| Field | Value |
|-------|-------|
| Existing skill | Any skill with run_settings configured |
| Original model | GPT-4 Turbo |
| Original reasoning | Medium |
| Original max tokens | 5000 |
| Original context toggle | OFF |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open existing skill with configured run_settings | Skill editor displays with current version |
| 2 | Expand "Run settings" → Verify current settings (model, reasoning, tokens, context) | All settings display correctly |
| 3 | Make a small change to instructions (not run settings) | Instructions updated |
| 4 | Click "Save as new version" button | Version save dialog appears |
| 5 | Enter version name or accept default → Confirm save | New version created, success notification |
| 6 | Verify version dropdown now shows new version as active | New version selected |
| 7 | Expand "Run settings" accordion | Run settings section displays |
| 8 | Verify Model shows the same model as original version (GPT-4 Turbo) | Model copied |
| 9 | Open Model settings → Verify REASONING level is Medium | Reasoning copied |
| 10 | Verify Max tokens is 5000 | Max tokens copied |
| 11 | Verify "Include project context" toggle is OFF | Context toggle copied |
| 12 | Switch version dropdown to previous version → Expand Run settings | Previous version settings unchanged |
| 13 | Switch back to new version → Expand Run settings | New version settings match original |

## Expected Final State

- New version created with identical run_settings as the source version
- Both versions maintain their own run_settings independently
- All fields (model, reasoning, tokens, context) copied correctly

## Pass/Fail Criteria

**Pass:**
- New version has identical run_settings as source version
- Model selection copied correctly
- Reasoning level copied correctly
- Max tokens copied correctly
- Project context toggle state copied correctly
- Both versions are independent

**Fail:**
- New version has null or default run_settings
- Any setting is lost during copy
- New version inherits only partial settings
- Versions are not independent
