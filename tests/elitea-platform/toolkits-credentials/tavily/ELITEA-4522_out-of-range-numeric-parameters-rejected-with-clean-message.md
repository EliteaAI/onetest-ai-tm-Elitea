---
id: ELITEA-4522
title: "Verify out-of-range numeric parameters on the Test page are rejected with a clean, user-friendly message"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid API key, open on its "Test Toolkit" page

## Test Data

| Field | Out-of-range value |
|-------|---------------------|
| Web crawl Max Depth | 999 (ceiling 2) |
| Web crawl Limit | 999 (ceiling 20) |
| Web map Limit | 999 (ceiling 50) |
| Web map Max Depth | 999 (ceiling 2) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select Web crawl, fill a valid Url, set Max Depth to 999, attempt to run | Run is rejected with a clear, user-friendly message (e.g. stating the valid range), not a raw internal/implementation error |
| 2 | Repeat for Web crawl Limit set above 20 | Same clean rejection behavior |
| 3 | Repeat for Web map Limit set above 50 | Same clean rejection behavior |
| 4 | Repeat for Web map Max Depth set above 2 | Same clean rejection behavior |
| 5 | Observe the "Run Test" button state when a field value is already known to be out of range | Button is disabled or submission is otherwise blocked by inline validation before running |

## Expected Final State

All documented numeric ceilings on the Test page are enforced with clean, user-facing messages.

## Pass/Fail Criteria

**Pass:**
- Every out-of-range value is rejected with a clean message
- Submission is blocked inline when possible

**Fail:**
- Any out-of-range value is accepted
- The error message exposes raw internal/implementation details
