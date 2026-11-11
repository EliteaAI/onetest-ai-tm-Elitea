---
id: ELITEA-2651
title: "Default Modules UI Structure and Toggle State Persistence"
priority: critical
type: functional
module: default-modules
status: draft
execution_type: manual
tags: [feat:settings, feat:modules, feat:web-search, eng:frontend, eng:automation, issue:6122, issue:6980, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2651: Default Modules UI Structure and Toggle State Persistence

**Module:** Default Modules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Default Modules section UI structure (table, columns, modules, toggles) and that toggle states persist after page refresh and re-login.

**Coverage:**
- Default Modules section visibility in Settings → General
- Table structure with Module, Chats, and Agents columns
- All 11 modules displayed with toggle switches (including Web Search)
- Toggle state persistence after page refresh
- Toggle state persistence after logout and re-login

## Preconditions

- Logged into {{base_url}}
- User has permission to modify project settings
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Expected modules (11 total):
1. Image Creation
2. Data Analysis
3. Agent & Pipeline Builder
4. Skill Builder
5. Project Context Builder
6. Ask User
7. Planner
8. Python Sandbox
9. Swarm Mode
10. Smart Tools Selection
11. Web Search

Test configuration:
- Enable: Image Creation (Chats), Data Analysis (Agents), Planner (both), Web Search (Chats)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → General. | Settings page loads successfully. |
| 2 | Locate the "Default Modules" section on the page. | Default Modules section is visible. |
| 3 | Verify the table has 3 columns. | Table has columns: "Module", "Chats", "Agents". |
| 4 | Count the number of module rows in the table. | Exactly 11 module rows are displayed, including Web Search. |
| 5 | Verify each module row has toggle switches in both Chats and Agents columns. | Each row has 2 toggle switches. All toggles are OFF by default. |
| 6 | Enable Image Creation toggle for Chats column. | Toggle switches to ON state. |
| 7 | Enable Data Analysis toggle for Agents column. | Toggle switches to ON state. |
| 8 | Enable Planner toggle for both Chats and Agents columns. | Both toggles switch to ON state. |
| 9 | Enable Web Search toggle for Chats column. | Toggle switches to ON state. |
| 10 | Refresh the page (F5). | Page reloads. |
| 11 | Verify all enabled toggles are still ON after refresh. | Image Creation (Chats), Data Analysis (Agents), Planner (both), Web Search (Chats) are ON. All other toggles are OFF. |
| 12 | Log out of the application. | User is logged out successfully. |
| 13 | Log back in with the same credentials. | User is logged in successfully. |
| 14 | Navigate to Settings → General → Default Modules. | Default Modules section is displayed. |
| 15 | Verify all toggle states persisted after re-login. | Image Creation (Chats), Data Analysis (Agents), Planner (both), Web Search (Chats) are ON. All other toggles are OFF. |

## Expected Final State

- Default Modules section displays correctly with 11 modules (including Web Search) and proper table structure
- All configured toggle states persist after page refresh and re-login

## Pass/Fail Criteria

**Pass:**
- Default Modules section is visible with correct table structure (3 columns, 11 rows)
- Each module, including Web Search, has toggle switches for both Chats and Agents columns
- Toggle states persist after page refresh
- Toggle states persist after logout and re-login

**Fail:**
- Section not visible or table structure incorrect
- Missing modules or toggle switches
- Toggle states reset after page refresh
- Toggle states reset after logout/re-login
