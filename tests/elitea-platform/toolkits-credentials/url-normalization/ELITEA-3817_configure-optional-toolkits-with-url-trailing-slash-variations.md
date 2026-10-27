---
id: ELITEA-3817
title: "Configure optional toolkits with URL trailing slash variations"
priority: medium
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
- Valid credentials for optional toolkits are available (as applicable)

## Test Data

| Toolkit Type | URL Field Name | Test URL (with trailing slash) | Priority in Issue |
|--------------|----------------|-------------------------------|-------------------|
| Azure DevOps Repositories | organization_url | `https://dev.azure.com/my-org/` | Follow-up |
| Azure DevOps Test Plans | organization_url | `https://dev.azure.com/my-org/` | Follow-up |
| Azure DevOps Wiki | organization_url | `https://dev.azure.com/my-org/` | Follow-up |
| Azure DevOps Work Items | organization_url | `https://dev.azure.com/my-org/` | Follow-up |
| Bitbucket | url | `https://bitbucket.example.com/` | Follow-up |
| TestRail | url | `https://testrail.example.com/` | Follow-up |
| ServiceNow | base_url | `https://company.service-now.com/` | Follow-up |
| Rally | server | `https://rally1.rallydev.com/` | Follow-up |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Create Azure DevOps credential with organization_url: `https://dev.azure.com/my-org/` | Credential form accepts URL with trailing slash |
| 3 | Enter valid credentials for Azure DevOps | Credentials accepted |
| 4 | Click "Check Connection" | Connection check initiates |
| 5 | Verify connection result (if normalization implemented) | Connection succeeds, or shows appropriate error unrelated to trailing slash |
| 6 | Save credential | Credential saved successfully |
| 7 | Navigate to Toolkits & Indexes and create Azure DevOps Repositories toolkit | Toolkit created and linked to credential |
| 8 | Repeat steps 2-7 for Azure DevOps Test Plans | Test Plans credential and toolkit configured |
| 9 | Repeat steps 2-7 for Azure DevOps Wiki | Wiki credential and toolkit configured |
| 10 | Repeat steps 2-7 for Azure DevOps Work Items | Work Items credential and toolkit configured |
| 11 | Create Bitbucket credential with url field: `https://bitbucket.example.com/` | Bitbucket credential configured |
| 12 | Create Bitbucket toolkit linked to credential | Bitbucket toolkit created |
| 13 | Create TestRail credential with url field: `https://testrail.example.com/` | TestRail credential configured |
| 14 | Create TestRail toolkit linked to credential | TestRail toolkit created |
| 15 | Create ServiceNow credential with base_url field: `https://company.service-now.com/` | ServiceNow credential configured |
| 16 | Create ServiceNow toolkit linked to credential | ServiceNow toolkit created |
| 17 | Create Rally credential with server field: `https://rally1.rallydev.com/` | Rally credential configured |
| 18 | Create Rally toolkit linked to credential | Rally toolkit created |
| 19 | For Azure DevOps Work Items toolkit, execute a runtime tool call in an Agent | Tool executes successfully (if normalization implemented) |
| 20 | For Bitbucket toolkit, execute a runtime tool call in an Agent | Tool executes successfully (if normalization implemented) |

## Expected Final State

- All 8 optional toolkits accept URLs with trailing slashes in configuration
- Check Connection works for all toolkits (if URL normalization is implemented for them)
- If normalization is not yet implemented for a toolkit, appropriate error handling exists
- No crashes or unexpected behavior when configuring with trailing slashes
- Runtime execution works for toolkits where it's applicable

## Pass/Fail Criteria

**Pass:**
- All 8 optional toolkits accept URL configuration with trailing slashes
- Check Connection succeeds for toolkits where normalization is implemented
- For toolkits where normalization is NOT yet implemented, system provides clear feedback (either connection succeeds anyway, or error is unrelated to trailing slash)
- No system crashes or unexpected errors
- Runtime execution works for applicable toolkits (Azure DevOps Repos/Work Items, Bitbucket)
- Configuration saves successfully for all toolkits

**Fail:**
- Any toolkit rejects URL with trailing slash at configuration level
- System crashes when configuring with trailing slashes
- Unclear or misleading error messages about URL format
- Runtime execution fails due to trailing slash for toolkits where normalization should be implemented
- Configuration fails to save for any toolkit

**Note:** This test case covers follow-up/optional toolkits per issue #6810. Some may not have URL normalization implemented yet, which is acceptable per the issue scope. The test verifies graceful handling.
