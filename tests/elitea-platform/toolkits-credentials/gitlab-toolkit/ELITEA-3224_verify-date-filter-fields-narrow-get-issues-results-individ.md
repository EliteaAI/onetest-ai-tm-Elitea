---
id: ELITEA-3224
title: "Verify date filter fields narrow get_issues results individually and in combination"
priority: high
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit and GitLab Org toolkit configured
- Test repository has issues created/updated across at least 2 different weeks
- At least one issue with a known, precise `created_at`/`updated_at` timestamp

## Test Data

| Field | Value |
|-------|-------|
| `created_after` | 30 days ago |
| `created_before` | today |
| `updated_after` | date within the test window |
| `updated_before` | date within the test window |
| Boundary timestamp | Exact `created_at`/`updated_at` of a known issue |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with only `created_after=<30 days ago>` set | Only issues created on/after that date are returned |
| 2 | Invoke `get_issues` with only `created_before=<today>` set | Only issues created on/before that date are returned |
| 3 | Invoke `get_issues` with both `created_after` and `created_before` set together | Only issues created within that window are returned |
| 4 | Invoke `get_issues` with only `updated_after=<date>` set | Results are filtered by last-update time rather than creation time |
| 5 | Invoke `get_issues` with only `updated_before=<date>` set | The same upper-bound filtering applies to update time |
| 6 | Invoke `get_issues` with both `updated_after` and `updated_before` set together | Only issues updated within that window are returned |
| 7 | Using an issue with a known `created_at`/`updated_at`, set `created_after`/`updated_after` to exactly that timestamp | The boundary behavior (inclusive or exclusive) is observed and confirmed consistent with `created_before`/`updated_before` at the boundary |
| 8 | Combine `created_after`/`created_before` together with `updated_after`/`updated_before` in the same call | Both the creation-time and update-time windows are applied together (AND semantics) |
| 9 | Repeat steps 1, 3, and 6 against the GitLab Org toolkit | Same filtering behavior is observed |

## Expected Final State

All four date-filter fields correctly narrow results individually, at their boundaries, and in combination, on both toolkits.

## Pass/Fail Criteria

**Pass:**
- Each date field filters results correctly on its own
- Combined creation-time and update-time windows apply together
- Boundary inclusivity/exclusivity is consistent across `created_after`/`created_before`/`updated_after`/`updated_before`
- GitLab Org toolkit matches this behavior

**Fail:**
- A date filter has no effect or filters incorrectly
- Combined date filters ignore one of the windows
- Boundary behavior is inconsistent between fields
