---
id: ELITEA-3818
title: "Performance test with multiple toolkits configured with various URL formats"
priority: medium
type: performance
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to Admin Panel, Agents, and Pipelines sections
- Valid credentials for multiple toolkits are available

## Test Data

| Scenario | Configuration |
|----------|---------------|
| Multiple toolkits | 10+ toolkit configurations (mix of Jira, GitHub, Salesforce, SonarQube, Azure DevOps, etc.) |
| URL formats | Mix of URLs with and without trailing slashes |
| Agent configuration | Agent with 5+ different toolkits enabled |
| Pipeline configuration | Pipeline with 10+ toolkit steps |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Admin Panel > Toolkits section | Page loads within acceptable time |
| 2 | Configure 10+ toolkits with mix of URL formats (some with trailing slash, some without) | All configurations accepted |
| 3 | For each toolkit, click "Check Connection" | All Check Connection operations complete within reasonable time (e.g., < 5 seconds each) |
| 4 | Verify all 10+ toolkits saved successfully | All configurations persist correctly |
| 5 | Navigate to toolkit list page and load all configured toolkits | List loads within acceptable time (e.g., < 3 seconds) |
| 6 | Create an Agent with 5+ different toolkits (all URLs with trailing slashes) | Agent creation completes normally |
| 7 | Enable multiple tools from each toolkit in the agent | Tools load and enable without performance degradation |
| 8 | Save the agent configuration | Save completes within acceptable time (e.g., < 2 seconds) |
| 9 | Execute the agent with prompts triggering all 5 toolkits | Agent execution completes within reasonable time |
| 10 | Measure agent response time for toolkit calls | Response times are acceptable (no significant performance impact from URL normalization) |
| 11 | Create a Pipeline with 10+ toolkit steps (mix of toolkit types, all URLs with trailing slashes) | Pipeline creation completes normally |
| 12 | Save the pipeline configuration | Save completes within acceptable time (e.g., < 3 seconds) |
| 13 | Execute the pipeline end-to-end | Pipeline execution completes within reasonable time |
| 14 | Measure total execution time | Execution time is acceptable (no significant overhead from URL normalization in each step) |
| 15 | Review system logs for any performance warnings | No performance-related warnings about URL processing |

## Expected Final State

- System handles 10+ toolkit configurations without performance issues
- Check Connection operations complete in reasonable time for all toolkits
- Agent with multiple toolkits loads and executes performantly
- Pipeline with multiple toolkit steps executes without significant delays
- URL normalization adds negligible overhead to toolkit operations

## Pass/Fail Criteria

**Pass:**
- 10+ toolkits can be configured simultaneously without errors
- Check Connection for each toolkit completes in < 5 seconds
- Toolkit list page loads in < 3 seconds with 10+ toolkits
- Agent with 5+ toolkits saves in < 2 seconds
- Agent execution with multiple toolkit calls completes in reasonable time (no 2x slowdown)
- Pipeline with 10+ toolkit steps executes without significant delays
- URL normalization overhead is negligible (< 5% impact on total execution time)
- No performance warnings in system logs

**Fail:**
- System slows down significantly with 10+ toolkits configured
- Check Connection operations timeout or take > 10 seconds
- Page loading times increase dramatically
- Agent or Pipeline save operations timeout
- Execution times are 2x or more slower due to URL normalization overhead
- System becomes unresponsive or crashes under load
- Performance degradation is noticeable to users
