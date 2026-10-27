---
id: ELITEA-3810
title: "Verify backward compatibility for pre-existing toolkit configurations without trailing slashes"
priority: high
type: regression
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- Test environment has pre-existing toolkit configurations created BEFORE the URL normalization enhancement
- Pre-existing toolkits are configured with URLs WITHOUT trailing slashes (standard format)
- Pre-existing toolkits include: Jira, GitHub, Salesforce, SonarQube
- Agent using at least one of the pre-existing toolkits exists

## Test Data

| Toolkit Type | Pre-existing URL Configuration | Status |
|--------------|-------------------------------|--------|
| Jira | `https://jiraeu.epam.com` | Configured before enhancement |
| GitHub | `https://github.example.com/api/v3` | Configured before enhancement |
| Salesforce | `https://company.my.salesforce.com` | Configured before enhancement |
| SonarQube | `https://sonar.example.com` | Configured before enhancement |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | After deployment of URL normalization enhancement, navigate to Admin Panel > Toolkits | Toolkits page loads successfully |
| 2 | Verify all pre-existing Jira toolkit configurations are visible | Pre-existing Jira toolkit(s) appear in list |
| 3 | Open pre-existing Jira toolkit configuration | Configuration opens with saved URL (no trailing slash) |
| 4 | Click "Check Connection" on pre-existing Jira toolkit | Connection check succeeds (no regression) |
| 5 | Execute a tool call from pre-existing Jira toolkit | Tool executes successfully (no regression) |
| 6 | Repeat steps 2-5 for GitHub toolkit | GitHub toolkit works correctly |
| 7 | Repeat steps 2-5 for Salesforce toolkit | Salesforce toolkit works correctly |
| 8 | Repeat steps 2-5 for SonarQube toolkit | SonarQube toolkit works correctly |
| 9 | Open an existing Agent that uses one of the pre-existing toolkits | Agent configuration opens |
| 10 | Execute the Agent with toolkit calls | Agent runs successfully, toolkit calls succeed |
| 11 | Verify agent execution log shows no errors | No toolkit-related errors in logs |
| 12 | Create a new chat session with the Agent | Chat session starts |
| 13 | Send message triggering pre-existing toolkit | Toolkit executes successfully from Agent |

## Expected Final State

- All pre-existing toolkit configurations continue to work without issues
- No regression in Check Connection functionality
- No regression in toolkit tool execution
- Agents using pre-existing toolkits continue to function normally
- URL normalization enhancement is transparent to existing configurations

## Pass/Fail Criteria

**Pass:**
- All pre-existing toolkit configurations remain functional after deployment
- Check Connection succeeds for all pre-existing toolkits (no change in behavior)
- Tool execution succeeds for all pre-existing toolkits (no change in behavior)
- Agents using pre-existing toolkits run without errors
- No data loss or configuration corruption
- URLs without trailing slashes are left unchanged by normalization function

**Fail:**
- Any pre-existing toolkit configuration fails to load or shows errors
- Check Connection fails for any pre-existing toolkit after deployment
- Tool execution fails for any pre-existing toolkit after deployment
- Agents fail to execute due to toolkit issues
- Any configuration data is lost or corrupted
- Normalization function incorrectly modifies URLs without trailing slashes
