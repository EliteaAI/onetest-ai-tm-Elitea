---
id: ELITEA-4151
title: Verify max_skills_per_agent configuration is reflected in API response
priority: High
objective: Verify that the max_skills endpoint returns the configured max_skills_per_agent value and UI uses it as single source of truth
preconditions: |
  - User is logged in with appropriate permissions
  - Access to API testing tools or browser developer tools
  - max_skills_per_agent is configured to a known value (e.g., 50)
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "api", "configuration", "S11", "backend"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Set max_skills_per_agent to 50 in backend configuration
2. Make an API call to GET /api/v2/application_skills (or equivalent endpoint)
3. Inspect the response body
4. Verify the max_skills field is present
5. Verify the max_skills value matches the configuration
6. Change max_skills_per_agent to a different value (e.g., 30)
7. Restart services if required
8. Make the same API call again
9. Verify the max_skills field now shows 30
10. Open agent editor in UI and verify counter shows new limit

## Expected Results

- API response includes max_skills field
- max_skills value in response matches backend configuration (50)
- After changing configuration to 30, API returns max_skills: 30
- UI skill counter reflects the API value (e.g., "x/50" then "x/30" after change)
- No hardcoded limits in UI (UI reads from API response)
- API response is consistent across different endpoints that expose skill limits
