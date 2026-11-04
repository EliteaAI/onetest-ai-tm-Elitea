---
id: ELITEA-4435
title: "Verify direct URL navigation to analytics page works correctly"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, navigation, url-routing]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User knows or can copy analytics URL for a specific skill run
- URL format: `/skills/:tab/:skillId/history/analytics`
- User is logged in

## Test Data

| Field | Value |
|-------|-------|
| URL Pattern | `/skills/:tab/:skillId/history/analytics` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to analytics page via normal flow | Analytics page displays |
| 2 | Copy URL from browser address bar | URL copied |
| 3 | Note the run's metadata: date, version, model | Metadata recorded |
| 4 | Close analytics page or navigate away | Leave analytics page |
| 5 | Paste copied URL directly into browser address bar | URL pasted |
| 6 | Press Enter to navigate | Navigation initiates |
| 7 | Verify analytics page loads | Page displays |
| 8 | Verify correct run data loads | Same run as originally viewed |
| 9 | Verify metadata matches: date, version, model | Metadata identical |
| 10 | Verify no authentication errors | No login required (user already authenticated) |
| 11 | Verify URL parameters parsed correctly | Page interprets URL correctly |
| 12 | Verify default tab (Costs) opens | Default tab active |
| 13 | Verify no redirect loops or 404 errors | Navigation stable |

## Expected Final State

Direct URL navigation:
- Analytics page loads with correct run data
- No authentication errors (if user logged in)
- URL parameters parsed correctly
- Default tab (Costs) opens
- No redirect loops or 404 errors
- Data matches original run

## Pass/Fail Criteria

**Pass:**
- Direct URL navigation works
- Correct run data loads
- No authentication errors
- URL parsed correctly
- Default tab opens
- No navigation errors

**Fail:**
- Direct URL fails
- Wrong run data loads
- Authentication error
- URL parsing error
- Tab doesn't open
- 404 or redirect loop
