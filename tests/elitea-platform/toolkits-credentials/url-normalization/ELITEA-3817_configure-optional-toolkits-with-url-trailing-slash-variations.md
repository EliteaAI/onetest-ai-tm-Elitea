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
- User has access to Admin Panel > Toolkits section
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
| 1 | Navigate to Admin Panel > Toolkits section | Toolkits page loads successfully |
| 2 | Configure Azure DevOps Repositories toolkit with organization_url: `https://dev.azure.com/my-org/` | Configuration form accepts URL with trailing slash |
| 3 | Enter valid credentials for Azure DevOps Repositories | Credentials accepted |
| 4 | Click "Check Connection" | Connection check initiates |
| 5 | Verify connection result (if normalization implemented) | Connection succeeds, or shows appropriate error unrelated to trailing slash |
| 6 | Save configuration | Configuration saved successfully |
| 7 | Repeat steps 2-6 for Azure DevOps Test Plans | Test Plans toolkit configured and Check Connection works |
| 8 | Repeat steps 2-6 for Azure DevOps Wiki | Wiki toolkit configured and Check Connection works |
| 9 | Repeat steps 2-6 for Azure DevOps Work Items | Work Items toolkit configured and Check Connection works |
| 10 | Repeat steps 2-6 for Bitbucket (url field) | Bitbucket toolkit configured and Check Connection works |
| 11 | Repeat steps 2-6 for TestRail (url field) | TestRail toolkit configured and Check Connection works |
| 12 | Repeat steps 2-6 for ServiceNow (base_url field) | ServiceNow toolkit configured and Check Connection works |
| 13 | Repeat steps 2-6 for Rally (server field) | Rally toolkit configured and Check Connection works |
| 14 | For Azure DevOps Work Items, execute a runtime tool call in an Agent | Tool executes successfully (if normalization implemented) |
| 15 | For Bitbucket, execute a runtime tool call in an Agent | Tool executes successfully (if normalization implemented) |

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
