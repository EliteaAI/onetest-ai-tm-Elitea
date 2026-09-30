---
id: ELITEA-3438
title: "Budget-Door Refusal Still Applies to Pipelines With an LLM Node"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, nfr:performance, story:6717, budget, regression]
requirements: [EliteaAI/elitea_issues#6717]
---
# ELITEA-3438: Budget-Door Refusal Still Applies to Pipelines With an LLM Node

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Confirm the new "LLM-free" fast path (`dispatch_may_use_llm()` in `elitea_core#458`) that skips the advisory `usage_gate_check` for provably LLM-free pipelines does **not** weaken enforcement for pipelines that actually contain an LLM node — this is the safety net the whole #6717 fix leans on, and it was left unverified in the PR's own test plan.

**Coverage:** Regression — `elitea_core#458`.

## Preconditions

- Ability to exhaust or simulate an exhausted predict budget for a test project/user
- A pipeline containing at least one `llm` node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With budget available, run predict on a pipeline containing an `llm` node. | Predict succeeds normally. |
| 2 | Exhaust the project/user's predict budget. | Budget is confirmed exhausted (e.g. via account/usage view). |
| 3 | Run predict again on the same LLM-containing pipeline. | Predict is refused at the door, same as pre-#6717 behavior — the LLM node means this dispatch does not qualify as "provably LLM-free," so the check still runs. |
| 4 | With budget still exhausted, run predict on a separate, genuinely LLM-free pipeline (only `code`/`router`/`state_modifier`/`printer`/`hitl` nodes, no `decision:` edge). | Predict is **not** refused by the advisory door (the check is correctly skipped for this dispatch) — confirm this doesn't itself indicate a budget-enforcement gap for pipelines that never touch an LLM in the first place. |

## Expected Final State

Budget-exhausted refusal still fires reliably for any pipeline that contains an LLM node; only structurally LLM-free pipelines skip the advisory pre-check.

## Pass/Fail Criteria

**Pass:**
- Step 3 is refused
- Step 4 succeeds without being incorrectly blocked

**Fail:**
- Step 3 is **not** refused (the LLM-free fast path incorrectly applied to a pipeline that has an LLM node) — this is the most severe possible outcome for #6717, since it would mean real LLM usage bypasses budget enforcement entirely
