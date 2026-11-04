---
id: ELITEA-4437
title: "Verify model displayed matches run execution model, not current skill settings"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, model-integrity, metadata]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill run was executed with specific model
- Skill may have been updated to use different model since
- User can access run history and analytics

## Test Data

| Field | Value |
|-------|-------|
| Test Scenario | Execute with Model A → Change skill to Model B → View Model A run analytics |
| Example Models | Execute with "claude-sonnet-5-5" → Change to "claude-opus-4-5" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure skill to use model "claude-sonnet-5-5" | Model set |
| 2 | Execute skill run with claude-sonnet-5-5 | Run completes |
| 3 | After run completes, change skill settings to use "claude-opus-4-5" | Skill now configured for opus |
| 4 | Verify skill editor shows claude-opus-4-5 | Current setting is opus |
| 5 | Navigate to Run History | Run History displays |
| 6 | Locate the original run (executed with sonnet) | Old run visible |
| 7 | Open Analytics for that run | Analytics page opens |
| 8 | Observe model displayed in header | Model shown in header |
| 9 | Verify header displays: "Model: claude-sonnet-5-5" | Shows EXECUTED model |
| 10 | Verify header does NOT display claude-opus-4-5 | Does NOT show current skill setting |
| 11 | Verify model accurate to historical execution | Historical accuracy maintained |
| 12 | Verify no confusion about which model generated results | Clear historical context |

## Expected Final State

Model display:
- Header displays: `Model: claude-sonnet-5-5` (executed model)
- Header does NOT display claude-opus-4-5 (current skill setting)
- Model accurate to historical execution
- No confusion about which model generated results

## Pass/Fail Criteria

**Pass:**
- Header shows executed model (claude-sonnet-5-5)
- Header does NOT show current skill setting (claude-opus-4-5)
- Historical accuracy maintained
- Clear which model generated the results

**Fail:**
- Header shows current skill setting instead of executed model
- Historical accuracy lost
- Confusion about which model generated results
- Incorrect model displayed
