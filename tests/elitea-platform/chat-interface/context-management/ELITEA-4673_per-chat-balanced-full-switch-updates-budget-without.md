---
id: ELITEA-4673
title: "Per-Chat Balanced Full Switch Updates Budget Without Changing Project Default"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Terminology Note (ticket re-check, 2026-11-11)

Per the AC3 correction (see ELITEA-4672), the Context window default is a **personal (per-user) setting applied across all projects**, not a per-project value. AC8 itself ("changing the chat's mode doesn't change the default, and vice versa") is unchanged and still active on the ticket — only the wording below is corrected from "project-level default" to "personal default" to match.

## Preconditions

- User is logged in to `{{base_url}}`
- An existing chat conversation uses a model whose context window is greater than 272,000 tokens

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Model | Any model with context window > 272,000 tokens (e.g., 400K or 1M) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the chat conversation on the large-window model. Open the Context management card. | Balanced mode shows Total window = 272,000 and an available/denominator value reduced by the ~1% safety margin. |
| 2 | Click the pencil/edit icon to open the Context Management modal. Select "Full". Click Save. | Modal shows the footer note "Applies to the next message in this conversation. Runs already in progress keep their original settings." Save succeeds. |
| 3 | Re-check the Context management card after saving. | Total window now equals the model's full window (e.g., 400,000 or 1,000,000), with a correspondingly larger available/denominator value. |
| 4 | Send a new message. | The larger budget is actually used; no premature summarization occurs even past the old 272,000-based threshold. |
| 5 | Use the quick segmented toggle (Balanced \| Full) directly on the Context management card/popover to switch back to Balanced. | The UI updates optimistically to Balanced immediately, then confirms after the backend responds. |
| 6 | Navigate to Settings → Memory (this user's personal setting, visible from any project). | The user's personal Context window default is unchanged from before this chat's mode was switched. |
| 7 | Change the personal default to a different mode than this chat's current mode. | This existing chat's own mode remains unaffected by the personal default change. |

## Expected Final State

The chat's window mode can be switched independently via both the modal and the quick toggle, the budget numbers update accordingly, and none of this affects — or is affected by — the user's personal default (AC8).

## Pass/Fail Criteria

**Pass:**
- Switching via the modal and via the quick toggle both correctly update Total window/available window
- The footer note about applying to the next message is shown
- The personal default and per-chat mode remain fully independent in both directions

**Fail:**
- Switching the chat's mode also changes the personal default (or vice versa)
- Total window / available window values do not update after the switch
- The quick toggle does not reflect an optimistic update or fails to reconcile with the backend
