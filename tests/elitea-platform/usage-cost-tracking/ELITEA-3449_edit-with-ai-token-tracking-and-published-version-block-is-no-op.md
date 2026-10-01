---
id: ELITEA-3449
title: "Edit with AI (Agent/Skill) records tokens on success; blocked attempt on a published version produces no billed row"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, edit-with-ai, agents, skills]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6568", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3449: Edit with AI (Agent/Skill) records tokens on success; blocked attempt on a published version produces no billed row

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify "Edit with AI" on an existing Agent/Skill records accurate tokens for a successful edit, and that attempting it on a **published** agent version is blocked client-side with zero billed usage (true no-op, not a billed-then-rejected call).

---

## Preconditions

- Logged in to {{base_url}} with edit permission on at least one unpublished agent and one published agent.

---

## Test Data

| Field | Value |
|-------|-------|
| Edit request (NL input) | "Add a chat starter asking the user for their order number" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing **unpublished** Agent → click "Edit with AI". | Modal opens with a natural-language request field. |
| 2 | Enter the test edit request and submit. | LLM proposes changes to specific fields (instructions, chat starters — capped at 4, skills — capped at 5). |
| 3 | Check Analytics/`usage_event` for the resulting row. | Input tokens include current field content + the edit request; output tokens reflect the proposed change; both non-zero. |
| 4 | Repeat steps 1–2 on an existing **Skill** with edit permission. | Same token-recording behavior confirmed for Skills. |
| 5 | Open a **published** Agent version → attempt "Edit with AI". | Action is blocked before any LLM call (per ELITEA-2759 / issue #5893). |
| 6 | Check Analytics/`usage_event` immediately after the blocked attempt. | No new row was created for the blocked attempt — confirms it is a true no-op, not a billed-then-rejected call. |

---

## Expected Final State

Successful Edit-with-AI calls (Agent and Skill) produce accurate token rows; the published-version block produces zero usage rows.

---

## Pass/Fail Criteria

**Pass:**
- Successful edits produce rows with plausible non-zero input/output tokens.
- The published-version block produces no `usage_event` row at all.

**Fail:**
- A successful edit's tokens are 0/missing.
- The blocked published-version attempt still produces a billed row.
