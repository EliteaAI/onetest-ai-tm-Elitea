---
id: ELITEA-3207
title: "Private/Share Toggle Is Visible Per Secret and Its State Persists"
priority: high
type: ui
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3207: Private/Share Toggle Visible Per Secret and Persists

**Module:** Secrets · **Priority:** High · **Type:** UI

**Objective:** Confirm each secret row exposes a share/private toggle, the toggle reflects the secret's actual current state, and changes persist across page reloads and sessions.

**Coverage:** TC-UI (toggle visible/persists per secret)

## Preconditions

- At least one personal-project secret exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Secrets page for a personal project. | Each secret row shows a share/private toggle control. |
| 2 | Note the toggle's current state for a given secret. | State matches the secret's actual share setting (verify via API if needed). |
| 3 | Flip the toggle (share → unshare, or vice versa). | UI updates immediately to reflect the new state. |
| 4 | Reload the page. | Toggle still shows the newly-set state (not reverted). |
| 5 | Log out and log back in, then revisit the page. | Toggle state still persists correctly. |

## Expected Final State

The toggle accurately reflects and persists the secret's share state across reloads and sessions.

## Pass/Fail Criteria

**Pass:**
- Toggle is present on every personal secret row, reflects true state, and persists across reload/re-login

**Fail:**
- Toggle missing, showing stale/incorrect state, or reverting after reload
