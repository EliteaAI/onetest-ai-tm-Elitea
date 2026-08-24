---
id: ELITEA-2686
title: "Tools Remain Alphabetically Sorted Within Each Group"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, grouping, sorting]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2686: Tools Remain Alphabetically Sorted Within Each Group

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify tools maintain strict alphabetical sorting within their assigned group after grouping is applied.

**Coverage:**
- Tools within each group are sorted alphabetically (A-Z)
- Sorting is consistent across all four groups
- No tool appears out of alphabetical order within its group

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- GitHub toolkit or similar toolkit with many tools exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open GitHub toolkit configuration and navigate to Tools section. | Tools section is displayed with grouped tools. |
| 2 | In the **Read** group, list all tool names displayed from top to bottom. | All tool names in the Read group are in **strict alphabetical order (A-Z)**. |
| 3 | In the **Create & update** group, list all tool names displayed from top to bottom. | All tool names in the Create & update group are in **strict alphabetical order (A-Z)**. |
| 4 | In the **Delete** group, list all tool names displayed from top to bottom. | All tool names in the Delete group are in **strict alphabetical order (A-Z)**. |
| 5 | In the **Execute** group, list all tool names displayed from top to bottom. | All tool names in the Execute group are in **strict alphabetical order (A-Z)**. |
| 6 | Open another SDK toolkit (e.g., Jira) and repeat verification for all groups. | Alphabetical sorting is consistent across different toolkit types. |
| 7 | Open Artifact toolkit and repeat verification for all groups. | Alphabetical sorting is consistent across different toolkit types. There is no **Execute** group (because there is no such toolkit.) |

## Expected Final State

All tools within each group are sorted alphabetically across all tested toolkits.

## Pass/Fail Criteria

**Pass:**
- Tools within each group are sorted alphabetically (A-Z)
- Sorting is consistent across all four groups
- No tool appears out of alphabetical order within its group
- Sorting behavior is consistent across different toolkit types

**Fail:**
- Any tool appears out of alphabetical order within its group
- Sorting is inconsistent between groups
- Different toolkits show different sorting behavior
