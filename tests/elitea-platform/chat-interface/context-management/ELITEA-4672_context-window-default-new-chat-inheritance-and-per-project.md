---
id: ELITEA-4672
title: "Context Window Default: New-Chat Inheritance and Per-Project Isolation"
priority: critical
type: functional
module: settings-memory
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## AC Update Note (ticket re-check, 2026-11-11)

Issue #6898's **AC3** was struck through on the ticket: "~When I select Full in Project A, it autosaves. After a reload Project A shows Full and Project B still shows Balanced (per-project isolation).~ - not actual, this is personal settings and applied to all project for user." The Context window default is a **single personal (per-user) setting that applies across every project**, not a per-project value. This case is rewritten accordingly: the former per-project isolation test (steps checking Project B is unaffected) is **removed and replaced** with a test that the setting is a single global value shared by all of the user's projects. AC2 and AC5 (default = Balanced; new chat inherits the setting) are otherwise unchanged and still covered.

## Merge Note

Merges former draft cases "Context window default applied to new chats" and "Per-project isolation of the Context window default" into a single flow — the isolation half was invalidated by the AC3 update above and replaced with a cross-project-consistency check in the opposite direction (one setting, not isolated per project).

## Preconditions

- User is logged in to `{{base_url}}` and has access to at least two distinct projects (A and B)
- This user has never explicitly changed their personal Context window default before this test

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/memory` |
| Project A | Any project accessible to this user |
| Project B | A different project accessible to the same user |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → Memory while in Project A (user has never configured this setting before). | "Balanced" is selected by default in the Context window radio group. |
| 2 | Select "Full" and wait for autosave, then reload the page. | No explicit Save button is required; after reload, the Context window radio still shows "Full". |
| 3 | Navigate to Chat and create a brand-new conversation in Project A. Send a test message, then open the Context management widget. | Window shows "Full" and Total window matches the active model's full context window (not capped at 272,000). |
| 4 | Switch to Project B in the project selector (same user, same personal setting). Open Settings → Memory. | Context window radio ALSO shows "Full" in Project B — the SAME value as Project A, because this is one personal setting for the user, applied to every project, not isolated per project. |
| 5 | Create a brand-new chat conversation in Project B. | The new chat in Project B also defaults to "Full" (the user's single personal setting), not a separate Project-B-specific value. |
| 6 | From Project B, change the setting to "Balanced". Switch back to Project A and re-open Settings → Memory. | Project A now also shows "Balanced" — confirming the change made from Project B applied globally to the same user's setting, visible from every project. |

## Expected Final State

The Context window default is a single personal (per-user) setting: it autosaves, survives a reload, is inherited by new chats, and shows/updates identically regardless of which project the user is currently viewing it from. There is no per-project isolation (per AC3's correction).

## Pass/Fail Criteria

**Pass:**
- Balanced is the default the first time this user ever views the setting
- Setting Full from Project A autosaves, survives a reload, and is inherited by new chats created in Project A
- The same value is visible from Project B without any additional action — confirming it is one personal setting, not per-project
- A change made from Project B is reflected back in Project A

**Fail:**
- Default shown is something other than Balanced for a user who has never set it
- The selection does not persist after reload
- A new chat does not inherit the user's current personal default window mode
- Project B shows a different value than Project A for the same user (isolation reappearing, contradicting the AC3 correction)
