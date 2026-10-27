---
id: ELITEA-4143
title: Verify search filters attached skills by skill name correctly
priority: High
objective: Verify that the search box above attached skills filters the list by skill name and displays matching results
preconditions: |
  - User is logged in with agent edit permissions
  - Agent exists with more than 8 skills attached (to display search box)
  - Attached skills have distinct names for testing
folder: Skills/Agent Skills/Skill Attach Limit
tags: ["skills", "agent-editor", "search", "filter", "S11", "usability"]
status: Ready
automation_status: Not Automated
execution_type: Manual
code_ref: null
---

## Test Steps

1. Open an agent that has at least 15-20 skills attached with varied names (e.g., "Database Query", "API Caller", "Data Parser", "Web Scraper", etc.)
2. Verify the search box is visible above the attached skills list
3. Note the full list of visible skills before searching
4. Click in the search box and type a partial skill name (e.g., "Data" to match "Database Query" and "Data Parser")
5. Observe the attached skills list as you type
6. Verify which skills remain visible
7. Clear the search box
8. Type a different search term that matches only one skill
9. Verify the filtering behavior
10. Type a search term that matches no skills

## Expected Results

- When typing "Data", only skills with "Data" in their name are displayed ("Database Query", "Data Parser")
- Skills that don't match the search term are hidden from the list
- Search is case-insensitive (typing "data" or "DATA" produces same results)
- Search filters in real-time as the user types (no need to press Enter)
- When search box is cleared, all attached skills are displayed again
- When searching for a term matching one skill, only that skill is displayed
- When searching for a term matching no skills, an empty state message is displayed
- The skill counter does not change (still shows total attached, e.g., "20/50", not filtered count)
