---
id: ELITEA-4682
title: "Agents and Pipelines Chat Panels Expose the Same Balanced Full Controls as Chat"
priority: high
type: integration
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## AC Update Note (ticket re-check, 2026-11-11)

Issue #6898's **AC11** was struck through on the ticket for the same personal-setting reason as AC10 (the deprecated read-only-permission case, not included in this batch): "~The same Balanced/Full controls work in Agents → Configuration chat and Pipelines chat panels.~ this is personal settings and applied to all project for user." Despite the formal AC being removed, **this case is kept active by explicit user decision** — the cross-panel parity check (and step 6's re-validation of ELITEA-0526/ELITEA-0528) retains standalone regression value independent of AC11.

## Merge Note

Merges former draft cases "Agents Configuration panel parity" and "Pipelines panel parity" — same assertion ("compact view mirrors Chat") against two hosts; parametrized into one case with a shared verification pattern.

## Preconditions

- User is logged in to `{{base_url}}`
- At least one Agent exists in the project with an accessible Configuration page and embedded chat/test panel
- At least one Pipeline exists in the project with an accessible chat/run panel

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` and `{{base_url}}/app/pipelines` |
| Test message | Any short message, e.g. "Hi" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open any Agent's Configuration page and locate its embedded chat/test panel. Send the test message and wait for the response. | A compact Context management indicator appears, showing the current window mode and token usage. |
| 2 | Click Edit and use the quick Balanced/Full toggle and then send another message. | The window mode switches successfully, is saved for this agent conversation, and the next response uses the newly selected mode's budget. |
| 3 | Compare the Usage totals (if shown in this compact view) against what would be expected for an equivalent conversation in the main Chat page. | Values are consistent with the same underlying per-conversation usage tracking used in Chat. |
| 4 | Open a Pipeline's chat/run panel. Trigger a run or send a message. | A compact Context management indicator appears with the current window mode and token usage. |
| 5 | Switch the window mode from this panel and trigger another run. | The change is saved and applied to subsequent runs; the pipeline's LLM node(s) use the budget corresponding to the newly selected window mode, not a hardcoded/legacy value. |
| 6 | Re-execute the scenarios from ELITEA-0526 (budget updates after each pipeline run) and ELITEA-0528 (budget does not reset after running a pipeline via chat) against this new widget. | Both scenarios still pass: budget correctly increases after each consecutive run, and does not reset to a near-zero state after a chat-triggered run. |

## Expected Final State

Both the Agent Configuration chat panel and the Pipelines chat panel expose the same window-mode switching and budget display behavior as the main Chat page, and the existing pipeline-related budget-update behaviors (ELITEA-0526, ELITEA-0528) continue to pass under the new widget.

## Pass/Fail Criteria

**Pass:**
- Compact Context management indicator appears in both the Agent Configuration panel and the Pipelines panel
- Window mode can be switched from both panels and is respected on the next message/run
- Pipeline LLM nodes respect the selected window mode; ELITEA-0526 and ELITEA-0528 scenarios still pass
- Usage totals (if present) are consistent with the Chat page's tracking

**Fail:**
- No Context management indicator appears in either panel
- Window mode switching is unavailable, does not take effect, or is ignored by pipeline LLM nodes
- ELITEA-0526 or ELITEA-0528 scenarios regress under the new widget
