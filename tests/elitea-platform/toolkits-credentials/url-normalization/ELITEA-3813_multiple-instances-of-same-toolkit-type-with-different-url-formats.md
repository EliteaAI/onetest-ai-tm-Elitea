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
- User has access to Admin Panel > Toolkits section
- Valid credentials for two different Jira instances are available

## Test Data

| Toolkit Instance | URL Configuration | Description |
|------------------|-------------------|-------------|
| Jira Instance 1 | `https://jira1.example.com` (no trailing slash) | First Jira toolkit |
| Jira Instance 2 | `https://jira2.example.com/` (with trailing slash) | Second Jira toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Configure first Jira toolkit with URL WITHOUT trailing slash: `https://jira1.example.com` | First Jira toolkit configuration created |
| 3 | Enter credentials for first Jira instance | Credentials accepted |
| 4 | Click "Check Connection" for first toolkit | Connection succeeds |
| 5 | Save first Jira toolkit configuration | Configuration saved successfully |
| 6 | Configure second Jira toolkit with URL WITH trailing slash: `https://jira2.example.com/` | Second Jira toolkit configuration created |
| 7 | Enter credentials for second Jira instance | Credentials accepted |
| 8 | Click "Check Connection" for second toolkit | Connection succeeds (URL normalized) |
| 9 | Save second Jira toolkit configuration | Configuration saved successfully |
| 10 | Verify both Jira toolkits appear in toolkit list | Both toolkits visible and distinguishable |
| 11 | Create an Agent and add first Jira toolkit | First Jira toolkit added to agent |
| 12 | Execute a tool call using first Jira toolkit | Tool executes successfully, connects to jira1.example.com |
| 13 | Create another Agent and add second Jira toolkit | Second Jira toolkit added to different agent |
| 14 | Execute a tool call using second Jira toolkit | Tool executes successfully, connects to jira2.example.com (URL normalized) |
| 15 | Verify each agent uses correct Jira instance | Each agent connects to its respective Jira instance |
| 16 | Execute tools from both agents in parallel/sequence | Both work independently without interference |

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
