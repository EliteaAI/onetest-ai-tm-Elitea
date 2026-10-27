---
id: ELITEA-3818
title: "Jira Credential URL Normalization - Full Flow"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

# ELITEA-3818: Jira Credential URL Normalization - Full Flow

**Module:** toolkits-credentials · **Priority:** critical · **Type:** functional

**Objective:** Verify that Jira credentials accept Base URLs with trailing slashes, normalize them server-side, and work correctly in Agent runtime execution without URL-related errors.

---

## Preconditions

- User is logged in to the Elitea platform
- User has access to Credentials, Toolkits & Indexes, and Agents sections
- Valid Jira credentials are available (username and API token)
- Base URL: `https://jiraeu.epam.com`

---

## Test Data

| Field | Value |
|-------|-------|
| Credential Display Name | autotest_jira_trailing_slash |
| Credential ID | autotest-jira-trailing-slash |
| Base URL | `https://jiraeu.epam.com/` (with single trailing slash) |
| Auth Type | Basic |
| Username | Valid Jira username |
| API Token | Valid Jira API token |
| Toolkit Name | autotest_jira_toolkit |
| Agent Name | autotest_jira_agent |

---

## Steps

### Part 1: Create Credential with trailing slash

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" button | Credential type selection dialog opens |
| 3 | Select "Jira" credential type | New Jira Credential form opens |
| 4 | Enter Display Name: "autotest_jira_trailing_slash" | Field accepts input |
| 5 | Enter ID: "autotest-jira-trailing-slash" | Field accepts input |
| 6 | Enter Base URL WITH trailing slash: `https://jiraeu.epam.com/` | Field accepts URL with trailing slash, slash remains visible |
| 7 | Select Auth type: "Basic" | Basic auth fields appear |
| 8 | Enter valid Jira username | Field accepts input |
| 9 | Enter valid Jira API token | Field accepts input |
| 10 | Click "Test connection" button | Connection check initiates and succeeds (URL normalized server-side) |
| 11 | Click "Save" button | Success notification: "Credential saved successfully" |
| 12 | Verify credential appears in list | "autotest_jira_trailing_slash" visible in credentials list with Jira badge |

### Part 2: Create Toolkit

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 14 | Click "+ Toolkit" button | Toolkit type selection dialog opens |
| 15 | Select "Jira" toolkit type | New Jira Toolkit form opens |
| 16 | Enter Toolkit Name: "autotest_jira_toolkit" | Field accepts input |
| 17 | In "Jira Configuration" dropdown, select "autotest_jira_trailing_slash" | Credential is selected, form shows credential details |
| 18 | Click "Save" button | Success notification: "Toolkit saved successfully" |
| 19 | Verify toolkit appears in list | "autotest_jira_toolkit" visible in toolkits list |

### Part 3: Execute in Agent

| # | Action | Expected Result |
|---|--------|-----------------|
| 20 | Navigate to Agents section | Agents page loads successfully |
| 21 | Create new Agent: "autotest_jira_agent" | Agent creation form opens |
| 22 | Add toolkit "autotest_jira_toolkit" to Agent | Toolkit added to agent's configuration |
| 23 | Save Agent configuration | Agent saved successfully |
| 24 | Run Agent with a simple Jira query (e.g., "Get my Jira issues") | Agent starts execution, Jira toolkit is invoked |
| 25 | Verify Agent execution completes without URL-related errors | Agent execution successful, no errors about malformed URLs or double slashes |
| 26 | Check Agent logs for API calls | API calls use normalized URL (no double slashes in endpoint paths) |

---

## Expected Final State

- Jira credential is saved with trailing slash visible in Base URL field (UI does not strip)
- Test Connection succeeds (URL normalized server-side)
- Toolkit successfully references the credential
- Agent executes Jira toolkit without URL-related errors
- API endpoint construction is correct (no double slashes)

---

## Pass/Fail Criteria

**Pass:**
- Base URL field accepts trailing slash and keeps it visible in UI
- Test Connection succeeds with URL containing trailing slash
- Credential saves successfully
- Toolkit successfully links to credential
- Agent execution completes without URL-related errors
- API calls use correctly normalized URLs (verified in logs)
- No error messages about malformed URLs, double slashes, or trailing slashes

**Fail:**
- Base URL field rejects or strips trailing slash in UI
- Test Connection fails due to trailing slash
- Credential fails to save
- Toolkit cannot reference credential
- Agent execution fails with URL-related errors
- Malformed API URLs with double slashes appear in logs

---

## Cleanup

- Delete Agent "autotest_jira_agent"
- Delete Toolkit "autotest_jira_toolkit"
- Delete Credential "autotest_jira_trailing_slash"
