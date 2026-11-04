---
id: ELITEA-4390
title: "Context Budget Message/Token Count Is Correct After Deselecting a Pipeline With 'Messages' State Disabled"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4390: Context Budget Message/Token Count Is Correct After Deselecting a Pipeline With 'Messages' State Disabled

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the exact reported defect (EliteaAI/elitea_issues#4840) no longer reproduces — deselecting a pipeline participant that has (or had) the "messages" state disabled does not inflate the Context Budget message or token count on the next chat message.

## Preconditions

- Logged in to {{base_url}}
- A pipeline with "messages" state disabled is available (or, if the toggle has been removed post-fix, a legacy pipeline that previously had it disabled)
- A second pipeline with "messages" state enabled is available for control comparison
- A Chat conversation exists where pipelines can be added as participants
- The Context Budget widget (tokens, Messages, Summaries) is visible in Chat

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline A | Pipeline with "messages" state disabled (or legacy equivalent) |
| Pipeline B (control) | Pipeline with "messages" state enabled |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Chat conversation and add Pipeline A as a participant. | Pipeline A appears correctly in the PARTICIPANTS panel. |
| 2 | Note the current Context Budget values (tokens, Messages, Summaries). | Baseline values are recorded. |
| 3 | Select Pipeline A in the chat and run it once; record the resulting Messages and token count. | Pipeline A executes successfully. Messages/token count update and are recorded. |
| 4 | Deselect Pipeline A in the chat (keep it in PARTICIPANTS). | Pipeline A is deselected without errors. |
| 5 | Send any normal chat message and immediately check the Context Budget widget. | Messages count increases by the expected amount only (no inflated +4-style jump) and token count is proportional to the actual message content — not inflated. |
| 6 | Record the Messages count delta and token count for this request. | Delta matches expected increment for one user message + one response; no anomalous spike. |
| 7 | Send one more message and check whether the Context Budget values change again without explanation. | Values continue to increment normally; no "self-correction" drop/jump is observed (confirming no transient inflation occurred). |
| 8 | Repeat Steps 1–7 using Pipeline B ("messages" enabled) as a control comparison. | Pipeline B shows the same correct, non-inflated behavior, confirming consistent counting logic regardless of the "messages" state configuration. |

## Expected Final State

Context Budget values remain accurate and consistent immediately after deselecting either pipeline and sending a follow-up message — no transient inflation of Messages or token count, and no delayed self-correction behavior for either Pipeline A or Pipeline B.

## Pass/Fail Criteria

**Pass:**
- After deselecting Pipeline A and sending a message, Messages count and token count reflect only the expected increment — no inflated/incorrect spike.
- The same message/token values do not change unexpectedly on the subsequent message (no "self-correction" pattern).
- Pipeline B (control) shows equivalent correct behavior.

**Fail:**
- After deselecting Pipeline A, the Context Budget shows an inflated message count (e.g., +4) or a disproportionately larger token count for that request.
- Values silently "correct themselves" on the next message, indicating the transient inflation defect still exists.
