---
id: ELITEA-3813
title: "Multiple instances of same toolkit type with different URL formats"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to Credentials and Toolkits & Indexes sections
- Valid credentials for two different Jira instances are available

## Test Data

| Toolkit Instance | URL Configuration | Description |
|------------------|-------------------|-------------|
| Jira Instance 1 | `https://jira1.example.com` (no trailing slash) | First Jira toolkit |
| Jira Instance 2 | `https://jira2.example.com/` (with trailing slash) | Second Jira toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Create first Jira credential with Display Name "Jira 1" and Base URL WITHOUT trailing slash: `https://jira1.example.com` | First credential form accepts input |
| 3 | Enter credentials for first Jira instance | Credentials accepted |
| 4 | Click "Check Connection" for first credential | Connection succeeds |
| 5 | Save first Jira credential | Credential saved successfully |
| 6 | Create second Jira credential with Display Name "Jira 2" and Base URL WITH trailing slash: `https://jira2.example.com/` | Second credential form accepts input |
| 7 | Enter credentials for second Jira instance | Credentials accepted |
| 8 | Click "Check Connection" for second credential | Connection succeeds (URL normalized) |
| 9 | Save second Jira credential | Credential saved successfully |
| 10 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 11 | Create first Jira toolkit "Jira Toolkit 1" and select credential "Jira 1" | First toolkit created and linked to first credential |
| 12 | Save first toolkit | First toolkit saved successfully |
| 13 | Create second Jira toolkit "Jira Toolkit 2" and select credential "Jira 2" | Second toolkit created and linked to second credential |
| 14 | Save second toolkit | Second toolkit saved successfully |
| 15 | Verify both Jira toolkits appear in toolkit list | Both toolkits visible and distinguishable |
| 16 | Create an Agent and add first Jira toolkit | First Jira toolkit added to agent |
| 17 | Execute a tool call using first Jira toolkit | Tool executes successfully, connects to jira1.example.com |
| 18 | Create another Agent and add second Jira toolkit | Second Jira toolkit added to different agent |
| 19 | Execute a tool call using second Jira toolkit | Tool executes successfully, connects to jira2.example.com (URL normalized) |
| 20 | Verify each agent uses correct Jira instance | Each agent connects to its respective Jira instance |
| 21 | Execute tools from both agents in parallel/sequence | Both work independently without interference |

## Expected Final State

- Two instances of same toolkit type (Jira) are configured successfully
- One instance uses URL without trailing slash, other uses URL with trailing slash
- Both instances work independently and correctly
- Each toolkit connects to its respective backend instance
- No URL format conflicts between multiple instances

## Pass/Fail Criteria

**Pass:**
- Both Jira toolkit instances configure successfully
- Check Connection succeeds for both instances
- Both instances save and persist correctly
- Each instance connects to correct backend (no cross-contamination)
- URL normalization works correctly for instance with trailing slash
- URL without trailing slash remains unchanged
- Both instances can be used simultaneously without errors

**Fail:**
- Unable to configure multiple instances of same toolkit type
- Check Connection fails for instance with trailing slash
- URL normalization interferes with instance identification
- Toolkits connect to wrong backend instances
- Configuration of one instance affects the other
- Any instance fails to execute tools correctly
