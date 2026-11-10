---
id: ELITEA-4468
title: "Import correctly re-links all 7 AI participant types by name, including Toolkit/MCP/public-Catalog entities, both into the same project and into a project that doesn't contain them"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, issue:6904, issue:7427, p0]
requirements: ["EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7427"]
---

# ELITEA-4468: Import correctly re-links all 7 AI participant types by name, including Toolkit/MCP/public-Catalog entities, both into the same project and into a project that doesn't contain them

**Module:** chat-interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an imported chat re-links by name all 7 AI participant types (Agent, Catalog Agent, Pipeline, Skill, Catalog Skill, Toolkit, MCP) when the target project contains matching names, and correctly adds none of them when the target project has no matching names. This also confirms the fix for bug #7427 (Toolkit/MCP/public-Catalog participants were previously not re-linked).

---

## Preconditions

- A project ("Project 1") containing: an Agent, an Agent available via the public Catalog, a Pipeline, a Skill, a Skill available via the public Catalog, a Toolkit, and an MCP — all available to be added to a chat.
- A second project ("Project 2") that does not contain any of the above 7 AI participants (confirm none exist there by name before testing).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Project 1, create a chat. Add as participants: 1) the Agent from the project, 2) the Agent from the Catalog, 3) the Pipeline, 4) the Skill from the project, 5) the Skill from the Catalog, 6) the Toolkit, 7) the MCP, 8) a User. Send at least one message. | Chat created with all 8 participants attached. |
| 2 | Export this chat "With attachments" (or "Without attachments" if it has no files — either is fine for this check). | Export completes successfully. |
| 3 | Import the exported file into Project 1 again (same project, where all 7 AI participants still exist by the same name). Check the resulting chat's participant list. | All 7 AI participant types — the Agent, the Catalog Agent, the Pipeline, the Skill, the Catalog Skill, the Toolkit, and the MCP — are re-added as real, functional participants (e.g. "View settings"/"Remove" work on each of them). This confirms the fix for bug #7427. The User from step 1 is never expected to be added (users are not re-added on import). |
| 4 | Import the same exported file into Project 2 (which contains none of the 7 AI participants by name). Check the resulting chat's participant list. | None of the 7 AI participant types are added — correct, since none exist by matching name in Project 2. No error, no placeholder; the chat remains usable. |

## Expected Final State

All 7 AI participant types re-link correctly by name when the target project has matching names (bug #7427 fix verified), and correctly do not re-link when the target project has no matching names.

## Pass/Fail Criteria

**Pass:**
- All 7 AI participant types re-link correctly in step 3; nothing re-links in step 4 (Project 2, no matches — correct, since no names match there).

**Fail:**
- Any of the 7 AI participant types — including Catalog Agent, Catalog Skill, Toolkit, or MCP — failing to re-link in step 3 (regression of the #7427 fix), or anything incorrectly re-linking in step 4.
