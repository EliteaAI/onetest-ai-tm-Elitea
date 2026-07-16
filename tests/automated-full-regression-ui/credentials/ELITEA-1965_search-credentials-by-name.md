---
id: ELITEA-1965
title: "Search Credentials by Name"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
automation_test_id: tests.ui.toolkits.test_credential_search_by_name.TestCredentialSearchByName.test_search_credentials_by_name
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/555
---

# ELITEA-1965: Search Credentials by Name

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the credentials search box correctly filters credentials by name, returning matching results and showing an empty/no-results state for non-existent queries.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential 1 | autotest_cred_alpha |
| Credential 2 | autotest_cred_beta |
| Credential 3 | autotest_cred_gamma |
| Partial search term | alpha |
| Full prefix search | autotest_cred |
| Non-existent search | nonexistent_xyz |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create credentials: "autotest_cred_alpha", "autotest_cred_beta", "autotest_cred_gamma" | All three credentials are created and visible in the list |
| 2 | Navigate to the credentials list | Credentials list page loads |
| 3 | Type "alpha" in the search box | Only "autotest_cred_alpha" is displayed in the results |
| 4 | Type "autotest_cred" in the search box | All three credentials (alpha, beta, gamma) are displayed |
| 5 | Type "nonexistent_xyz" in the search box | Empty state or no results message is displayed |
| 6 | Clear the search box | All credentials are listed again |

---

## Expected Final State

The search box correctly filters credentials dynamically; clearing the search restores the full list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Search results match the expected filtered set for each query; empty state is shown for no matches.

**Fail:**
- Any step produces an error or unexpected result.
- Search does not filter results, returns incorrect matches, or fails to show the empty state.
