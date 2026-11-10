---
id: ELITEA-4476
title: "All 7 AI participant types re-link on import, including Catalog/Toolkit/MCP (bug #7427 fix); cross-user author display is preserved"
priority: high
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, regression, cross-account, issue:6904, issue:7427, p1]
requirements: ["EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7427"]
---

# ELITEA-4476: All 7 AI participant types re-link on import, including Catalog/Toolkit/MCP (bug #7427 fix); cross-user author display is preserved

**Module:** chat-interface · **Priority:** High · **Type:** Regression

**Objective:** Confirm all 7 AI participant types (Agent, Catalog Agent, Pipeline, Skill, Catalog Skill, Toolkit, MCP) continue to re-link correctly on import — regression check for the bug #7427 fix — and that cross-user author display continues to be preserved correctly.

---

## Preconditions

- Project 1, containing an Agent, a Pipeline, a project-level Skill, a Catalog Agent, a Catalog Skill, a Toolkit, and an MCP — all available to User A.
- Project 2 (User B's own project), which also contains these same 7 AI participants, matched by the exact same names as in Project 1. This is deliberate: step 2 is testing cross-user author display, not participant matching again, so the 7 AI types must be able to match by name in Project 2 as well, isolating the author-display check from any name-matching gap.
- Two user accounts, "User A" and "User B".

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, create a chat with all 7 AI participant types added (Agent, Catalog Agent, Pipeline, Skill, Catalog Skill, Toolkit, MCP), plus a message sent by User A. Export it. Import it back into Project 1 (same project, as User A). | All 7 AI participant types are re-linked as real, functional participants — confirms the #7427 fix holds. |
| 2 | As User B, import the same exported file from step 1 into Project 2 (User B's own project, which — per Preconditions — contains these same 7 AI participants matched by name). | All 7 AI participant types are re-linked again in Project 2 (same as step 1, since they match by name there too). User B (the importer) is added as the chat's participant; User A is not added. User A's original message in the chat still correctly displays "User A" as the sender. |

## Expected Final State

All 7 AI participant types re-link correctly in both projects (bug #7427 fix verified), and cross-user author display remains correct in Project 2.

## Pass/Fail Criteria

**Pass:**
- All 7 AI participant types re-link in step 1 (Project 1) and again in step 2 (Project 2); in step 2, User B is the participant, User A is not, and User A's name is correctly preserved on her own message.

**Fail:**
- Any of the 7 AI participant types failing to re-link in step 1 or step 2 (regression of the #7427 fix), or User A's author display being lost/replaced with User B's in step 2.
