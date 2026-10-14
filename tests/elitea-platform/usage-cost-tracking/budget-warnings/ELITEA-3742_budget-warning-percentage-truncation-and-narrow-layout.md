---
id: ELITEA-3742
title: "Budget Warnings — Percentage Is Truncated, Not Rounded, and Banner Works on a Narrow Viewport"
priority: medium
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
size: S
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3742: Budget Warnings — Percentage Is Truncated, Not Rounded, and Banner Works on a Narrow Viewport

**Module:** Usage Cost Tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the displayed percentage never claims a level that hasn't been reached yet (it is truncated) and that the banner stays usable on a narrow screen (AC13).

**Coverage:**
- Truncation at 94.x% and 99.x%
- Severity consistent with the truncated %
- Layout at ~360px width

## Preconditions

- Logged in to `{{base_url}}`; Cost Budgets mode = **enforce**; dismissal switch **ON**
- A way to reach a fractional spend % near the boundaries (a small member limit, or a DevTools response override on the `budget_warning` call)

## Test Data

| Real spend | Displayed | Severity |
|------------|-----------|----------|
| 94.6% | 94% | elevated (amber) |
| 99.6% | 99% | critical (red) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Reach ~94.6% spend and reload | Banner reads "94%" with elevated severity, not "95%" / critical |
| 2 | Reach ~99.6% spend and reload | Banner reads "99%", not "100%" |
| 3 | Resize the browser to ~360px wide (DevTools device toolbar) | Text wraps, the % stays readable, and the close (X) button is fully visible and clickable |
| 4 | Click X | Banner is dismissed |

## Expected Final State

The banner is dismissed at narrow width, and the displayed % is never higher than the real %.

## Pass/Fail Criteria

**Pass:**
- Percent truncated in both cases, with severity matching the truncated value
- Banner readable and dismissible at 360px

**Fail:**
- Percent rounded up (shows 95% or 100%)
- Text overflows, or the X button is hidden or unclickable at narrow width
