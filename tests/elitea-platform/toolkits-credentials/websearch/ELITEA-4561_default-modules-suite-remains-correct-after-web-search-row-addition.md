---
id: ELITEA-4561
title: "Default Modules suite remains correct after Web Search row addition"
priority: medium
type: regression
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Project-admin access to Settings → General → Default Modules
- A non-public, non-admin test user account

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |
| Related existing cases | ELITEA-2641, ELITEA-2642, ELITEA-2643, ELITEA-2644, ELITEA-2645, ELITEA-2646, ELITEA-2647, ELITEA-2648, ELITEA-2649 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Re-run the Default Modules section UI verification scenario (ELITEA-2641) | Section renders correctly with the new Web Search row present |
| 2 | Re-run the toggle persistence after refresh scenario (ELITEA-2642), including the Web Search row | Toggle state persists after refresh |
| 3 | Re-run the applied-to-new-conversation/new-agent scenarios (ELITEA-2643/2644) | Defaults apply correctly including Web Search |
| 4 | Re-run the multiple-modules-enabled-simultaneously scenario (ELITEA-2645), including Web Search in the combination | All enabled modules (including Web Search) function together without conflict |
| 5 | Re-run the user-override-in-conversation/agent scenarios (ELITEA-2646/2647) | User overrides still work correctly |
| 6 | Re-run the private/team project-types scenario (ELITEA-2648) | Behavior is correct for both project types |
| 7 | Re-run the permissions and access control scenario (ELITEA-2649) as the non-public, non-admin test user | Default Modules (including the Web Search row) is shown as read-only |

## Expected Final State

All existing Default Modules behaviors continue to pass correctly with the Web Search row present.

## Pass/Fail Criteria

**Pass:**
- All re-run scenarios behave as previously verified, with no regression introduced by the Web Search row

**Fail:**
- Any re-run scenario breaks, mis-renders, or mis-counts modules due to the Web Search row
