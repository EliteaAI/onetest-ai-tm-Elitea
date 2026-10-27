---
id: ELITEA-3821
title: "Multiple Jira Toolkit Instances - URL Format Isolation"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

# ELITEA-3821: Multiple Jira Toolkit Instances - URL Format Isolation

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that multiple instances of the same toolkit type (Jira) can coexist with different URL formats (with/without trailing slash), each works correctly, and they do not interfere with each other.

---

## Preconditions

- User is logged in to the Elitea platform
- User has access to Credentials, Toolkits & Indexes, and Agents sections
- Valid credentials for two different Jira instances are available
- Two Jira instances: `https://jiraeu.epam.com` and `https://jira.example.com` (or two different projects on same instance)

---

## Test Data

| Instance | Credential Name | Base URL | Toolkit Name | Agent Name |
|----------|----------------|----------|--------------|------------|
| Jira 1 | autotest_jira1_no_slash | `https://jiraeu.epam.com` (no slash) | autotest_jira_toolkit1 | autotest_agent_jira1 |
| Jira 2 | autotest_jira2_with_slash | `https://jiraeu.epam.com/` (with slash) | autotest_jira_toolkit2 | autotest_agent_jira2 |

---

## Steps

### Part 1: Create First Credential (no trailing slash)

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads |
| 2 | Create Jira credential "autotest_jira1_no_slash" | Credential form opens |
| 3 | Enter Base URL WITHOUT trailing slash: `https://jiraeu.epam.com` | Field accepts URL |
| 4 | Enter valid Jira credentials for first instance | Credentials accepted |
| 5 | Click "Test connection" | Connection succeeds |
| 6 | Save credential | Credential "autotest_jira1_no_slash" saved successfully |

### Part 2: Create Second Credential (with trailing slash)

| # | Action | Expected Result |
|---|--------|-----------------|
| 7 | Create Jira credential "autotest_jira2_with_slash" | Credential form opens |
| 8 | Enter Base URL WITH trailing slash: `https://jiraeu.epam.com/` | Field accepts URL with slash |
| 9 | Enter valid Jira credentials for second instance | Credentials accepted |
| 10 | Click "Test connection" | Connection succeeds (URL normalized) |
| 11 | Save credential | Credential "autotest_jira2_with_slash" saved successfully |
| 12 | Verify both credentials visible in list | Both "autotest_jira1_no_slash" and "autotest_jira2_with_slash" listed |

### Part 3: Create Two Toolkits

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Navigate to Toolkits & Indexes | Toolkits page loads |
| 14 | Create Jira toolkit "autotest_jira_toolkit1" | Toolkit form opens |
| 15 | Select credential "autotest_jira1_no_slash" | Credential linked |
| 16 | Save toolkit | Toolkit "autotest_jira_toolkit1" saved |
| 17 | Create Jira toolkit "autotest_jira_toolkit2" | Toolkit form opens |
| 18 | Select credential "autotest_jira2_with_slash" | Credential linked |
| 19 | Save toolkit | Toolkit "autotest_jira_toolkit2" saved |
| 20 | Verify both toolkits visible in list | Both toolkits listed and distinguishable |

### Part 4: Execute in Separate Agents

| # | Action | Expected Result |
|---|--------|-----------------|
| 21 | Navigate to Agents section | Agents page loads |
| 22 | Create Agent "autotest_agent_jira1" with toolkit "autotest_jira_toolkit1" | Agent created with first Jira toolkit |
| 23 | Save Agent | Agent "autotest_agent_jira1" saved |
| 24 | Create Agent "autotest_agent_jira2" with toolkit "autotest_jira_toolkit2" | Agent created with second Jira toolkit |
| 25 | Save Agent | Agent "autotest_agent_jira2" saved |
| 26 | Execute first Agent with Jira query | Agent executes, connects to jiraeu.epam.com (no slash) |
| 27 | Verify first Agent execution completes successfully | No URL-related errors |
| 28 | Execute second Agent with Jira query | Agent executes, connects to jiraeu.epam.com/ (normalized) |
| 29 | Verify second Agent execution completes successfully | No URL-related errors |
| 30 | Verify each Agent uses correct Jira credential | Each agent connects to its respective credential configuration |
| 31 | Execute both Agents in sequence or parallel | Both work independently without interference |

---

## Expected Final State

- Two Jira credentials with different URL formats coexist
- Both Test Connections succeed
- Two Jira toolkits are created and linked to respective credentials
- Two Agents each use their respective Jira toolkit
- Both Agents execute successfully without URL-related errors
- Each Agent connects to its correct Jira credential (isolation verified)
- No interference between toolkit instances

---

## Pass/Fail Criteria

**Pass:**
- Both credentials save successfully with different URL formats
- Both Test Connections succeed
- Both toolkits link to their respective credentials
- Both Agents execute successfully
- Each Agent uses correct Jira credential (verified by API endpoint)
- No URL-related error messages
- Toolkit instances are properly isolated (no cross-contamination)
- API calls use correctly normalized URLs for each instance

**Fail:**
- One or both credentials fail to save
- Test Connection fails for either credential
- Toolkits cannot reference credentials
- Agent execution fails for either agent
- Agents interfere with each other or use wrong credentials
- URL-related error messages appear
- Malformed URLs with double slashes

---

## Cleanup

- Delete Agent "autotest_agent_jira1"
- Delete Agent "autotest_agent_jira2"
- Delete Toolkit "autotest_jira_toolkit1"
- Delete Toolkit "autotest_jira_toolkit2"
- Delete Credential "autotest_jira1_no_slash"
- Delete Credential "autotest_jira2_with_slash"
