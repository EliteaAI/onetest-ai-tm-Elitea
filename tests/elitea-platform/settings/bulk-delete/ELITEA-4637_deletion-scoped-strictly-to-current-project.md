---
id: ELITEA-4637
title: "Deletion is scoped strictly to the current project"
priority: critical
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Two projects (Project A and Project B) exist, each with Agents, Pipelines, Skills, Toolkits, Credentials, MCP servers, and Chats
- Project A has at least one resource shared in from another project (e.g., a shared Toolkit or Skill)
- User is Admin/owner on both projects

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Project A | QA-ProjectA |
| Project B | QA-ProjectB |
| Shared resource | Shared Toolkit from Project C |
| Entity type under test | Agents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record item counts for all seven entity types in Project A and Project B via Settings → General → Delete Project Data | Counts recorded for both projects |
| 2 | In Project A, select only "Agents," click "Delete selected data," type "DELETE," and click "Delete permanently" | Deletion completes successfully |
| 3 | Reopen Settings → General → Delete Project Data for Project A | Agents count in Project A is reduced to 0 (or expected remainder) |
| 4 | Open Settings → General → Delete Project Data for Project B | All counts in Project B unchanged from step 1 |
| 5 | Verify the shared resource in Project A | Shared resource still present and functional in Project A |

## Expected Final State

Only Project A's Agents are removed; Project B is entirely unaffected; shared-in resources in Project A remain intact.

## Pass/Fail Criteria

**Pass:**
- Project B counts unaffected
- Shared resource in Project A intact

**Fail:**
- Any cross-project data loss
- Shared resource removed
