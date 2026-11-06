---
id: ELITEA-4391
title: "Versions table reports full historical usage, including non-default, renamed, and deleted versions"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, versions]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4391: Versions table reports full historical usage, including non-default, renamed, and deleted versions

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Versions table on the Agent/Pipeline detail view shows every version actually executed in the selected period — including a version that is not the current default and one that has since been renamed or deleted — grouped by stable version identifier rather than by name, with correct metrics and default sort.

**Coverage:**
- Full historical version coverage (not scoped to current/default version)
- Correct RUNS / TOTAL TOKENS / COST per version row
- Grouping by stable version identifier, not display name
- Preservation of rows for renamed/deleted versions
- "Unknown version" fallback for missing attribution
- Default sort RUNS descending

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with at least 2 historically-run versions exists, one of which is NOT the current default version
- If possible, one historically-run version has since been renamed or deleted
- At least one run exists with missing/unresolvable version attribution (or this case is acknowledged as not reproducible if the environment cannot produce one)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with ≥2 historically-run versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view for the test Agent/Pipeline and locate the Versions table | Table renders with a VERSION, RUNS, TOTAL TOKENS, COST column set |
| 2 | Confirm both the current-default version and the non-default historically-run version appear as separate rows | Both versions listed, each with its own RUNS/TOTAL TOKENS/COST values that are not merged |
| 3 | If a version was renamed or deleted since execution, confirm its row still appears using the recorded name/identifier | Row persists; it is not dropped, not silently merged into another version, and not defaulted to showing the current entity version |
| 4 | Confirm rows for identical version identifiers are not duplicated under different display names (grouping is by identifier, not name) | Exactly one row per stable version identifier |
| 5 | If a run exists with missing version attribution, confirm it is shown as a distinct "Unknown version" row rather than being dropped or merged | "Unknown version" row present with its own RUNS/TOTAL TOKENS/COST |
| 6 | Observe the table's default sort order on initial load | Rows are sorted by RUNS descending by default |

## Expected Final State

The Versions table shows one row per every version (and "Unknown version" where applicable) that was actually executed during the selected period, regardless of current default status, correctly sorted by RUNS descending by default.

## Pass/Fail Criteria

**Pass:**
- All historically-run versions appear as distinct rows, including non-default and renamed/deleted versions
- Grouping uses stable version identifier, not display name
- Missing attribution shows as "Unknown version", never silently dropped or defaulted to the current version
- Default sort is RUNS descending

**Fail:**
- Non-default or deleted/renamed versions are missing, merged, or shown as the current default version
- Rows are grouped/duplicated by name instead of identifier
- Missing-attribution rows are dropped instead of shown as "Unknown version"
- Default sort is not RUNS descending
