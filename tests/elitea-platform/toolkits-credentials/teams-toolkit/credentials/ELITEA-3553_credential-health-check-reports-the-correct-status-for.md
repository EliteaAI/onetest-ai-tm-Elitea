---
id: ELITEA-3553
title: "Credential Health Check Reports the Correct Status for Each Token/Permission State"
priority: critical
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3553: Credential Health Check Reports the Correct Status for Each Token/Permission State

**Module:** Teams Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `check_connection` (GET `/me/joinedTeams`) returns the correct outcome for each Graph response scenario.

## Preconditions

- A Teams credential exists
- Ability to simulate or induce each response scenario below (expired token, token missing a scope, tenant/network conditions)

## Test Data

| Variant | Scenario |
|---|---|
| A | Valid token, Graph returns 200 |
| B | Token invalid or expired (401) |
| C | Token valid but missing `Team.ReadBasic.All` (403) |
| D | Graph returns any other non-2xx status |
| E | Graph request times out |
| F | Graph is unreachable (connection error) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run "Test Connection" for Variant A | Connection succeeds, no error |
| 2 | Run "Test Connection" for Variant B | Re-authorization is triggered/prompted, not a silent failure |
| 3 | Run "Test Connection" for Variant C | Error explicitly states access is forbidden due to missing Teams permissions |
| 4 | Run "Test Connection" for Variant D | Error message includes the returned HTTP status code |
| 5 | Run "Test Connection" for Variant E | Error indicates a connection timeout, not a generic failure |
| 6 | Run "Test Connection" for Variant F | Error indicates a connection error, not a generic failure |

## Expected Final State

Each scenario produces the specific, distinct outcome described above; none degrade to a generic/unhandled error.

## Pass/Fail Criteria

**Pass:**
- Each of the six scenarios produces exactly its documented, distinct outcome

**Fail:**
- Any scenario falls back to a generic error message, or a different scenario's outcome is shown
