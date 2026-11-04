---
id: ELITEA-4410
title: "Verify Run Header displays correct metadata (date, version, model)"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, metadata]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Run has completed successfully with metadata
- Run was executed with specific version and model

## Test Data

| Field | Value |
|-------|-------|
| Expected Header Format | `Run: [DD MMM YYYY, HH:MM AM/PM] · Version: [version_name] · Model: [model_name]` |
| Example | `Run: 14 Oct 2026, 12:24 PM · Version: v1.0 · Model: test1` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to any skill run analytics page | Analytics page opens |
| 2 | Observe the header section below breadcrumbs | Header section is visible |
| 3 | Note the run date/time displayed | Date/time shown in format: DD MMM YYYY, HH:MM AM/PM |
| 4 | Note the version name displayed | Version name displayed (e.g., "v1.0", "base") |
| 5 | Note the model name displayed | Model name displayed (e.g., "test1", "claude-sonnet-5-5") |
| 6 | Compare version with skill editor's current version | Version shown is from RUN EXECUTION, not current editor |
| 7 | Compare model with run's actual execution model | Model shown is from RUN EXECUTION, not current skill setting |
| 8 | Check all fields are populated | No "undefined", "null", or empty values |

## Expected Final State

Header displays:
- `Run: [execution date/time] · Version: [executed version] · Model: [executed model]`
- All fields populated with accurate historical data
- Version is from run execution, NOT current editor
- Model is from run execution, NOT current skill setting

## Pass/Fail Criteria

**Pass:**
- Header format matches: `Run: [date] · Version: [name] · Model: [name]`
- Date/time is accurate
- Version shown is the one used during execution
- Model shown is the one used during execution
- All fields populated (no undefined/null)

**Fail:**
- Header format incorrect
- Date/time missing or wrong
- Version shows current editor version instead of executed version
- Model shows current skill setting instead of executed model
- Any field undefined, null, or empty
