---
id: ELITEA-1199
title: "Jira Credential — Test Connection Validates Base URL Against Selected Hosting Type (Cloud / Server / Auto)"
priority: critical
type: functional
module: jira-toolkit-configuration
status: ready
execution_type: manual
tags: [feat:toolkits, int:jira, r-2.0.2]
requirements: []
---
# ELITEA-1199: Jira Credential — Test Connection Validates Base URL Against Selected Hosting Type (Cloud / Server / Auto)

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Test Connection on a Jira credential validates the Base URL against the selected Hosting type — returning an error when they are incompatible and succeeding when they match. Auto hosting applies no URL-based hosting validation.

**Coverage:**
- Cloud hosting + non-`*.atlassian.net` URL → error
- Server hosting + `*.atlassian.net` URL → error
- Auto hosting + any URL → no hosting validation error
- Matching URL + hosting type → successful connection (regression)

## Preconditions

- Logged in to {{base_url}}
- Access to Private or Team project credentials
- At least one Jira credential exists (or can be created) with an editable Hosting field and Base URL
- Test Connection button is available on the Jira credential configuration page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Jira credential configuration. Set **Hosting** to `Cloud`. Set **Base URL** to a self-hosted (non-atlassian.net) URL, e.g. `https://jira.yourcompany.com`. Click **Test Connection**. | Test Connection returns an error indicating the URL does not match the Cloud hosting type (e.g., URL must be *.atlassian.net for Cloud). Connection is not marked as successful. |
| 2 | Set **Hosting** to `Server`. Set **Base URL** to an Atlassian cloud URL, e.g. `https://yourcompany.atlassian.net`. Click **Test Connection**. | Test Connection returns an error indicating the URL does not match the Server hosting type (*.atlassian.net URLs are Cloud, not Server). Connection is not marked as successful. |
| 3 | Set **Hosting** to `Auto`. Set **Base URL** to a mismatched URL type (e.g., a self-hosted URL like `https://jira.yourcompany.com` or an atlassian.net URL). Click **Test Connection**. | Test Connection applies no hosting-based URL validation. The result is determined solely by the actual connectivity to the URL — no hosting mismatch error is returned regardless of the URL format. |
| 4 | Set **Hosting** to `Cloud`. Set **Base URL** to a valid atlassian.net URL, e.g. `https://yourcompany.atlassian.net`. Click **Test Connection**. | Test Connection passes the hosting validation check. The result reflects actual connectivity (success or network error) — no hosting mismatch error appears. |

## Expected Final State

Test Connection passes the hosting validation check. The result reflects actual connectivity (success or network error) — no hosting mismatch error appears.

## Pass/Fail Criteria

**Pass:**
- Cloud hosting with a non-atlassian.net URL returns a hosting mismatch error
- Server hosting with an atlassian.net URL returns a hosting mismatch error
- Auto hosting with a mismatched URL returns no hosting-related error
- Matching hosting + URL combination returns a successful connection result

**Fail:**
- Any hosting mismatch passes Test Connection without error
- Auto hosting incorrectly rejects a URL based on hosting type
- A valid matching combination unexpectedly fails
