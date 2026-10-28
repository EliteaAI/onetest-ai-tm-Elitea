---
id: ELITEA-4144
title: Verify search filters attached skills by description text correctly
priority: High
objective: Verify that the search box filters attached skills by description text in addition to skill name
preconditions: |
  - User is logged in with agent edit permissions
  - Agent exists with more than 8 skills attached
  - Attached skills have descriptions with varied content
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "search", "filter", "S11", "usability"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent that has at least 15 skills attached with descriptions containing different keywords
   - Example: Skill A - "Queries PostgreSQL databases"
   - Example: Skill B - "Calls REST APIs"
   - Example: Skill C - "Parses JSON and XML data"
2. Verify the search box is visible
3. Type a keyword that appears in some skill descriptions but not in skill names (e.g., "PostgreSQL")
4. Observe which skills remain visible
5. Clear the search
6. Type a keyword that appears in multiple descriptions (e.g., "data")
7. Verify the filtered results
8. Type a keyword that appears in both a skill name and another skill's description
9. Verify both skills are shown

## Expected Results

- Searching for "PostgreSQL" displays Skill A (even though "PostgreSQL" is not in the skill name)
- Search matches against both skill name and description text
- Searching for "data" shows both Skill C (name contains "data") and any other skills with "data" in description
- Search is case-insensitive for descriptions as well
- Skills matching in either name OR description are displayed (OR logic, not AND)
- Empty state is shown only when no skills match in either name or description
- Search filtering is fast and responsive even with many skills
