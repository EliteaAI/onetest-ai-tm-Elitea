---
id: ELITEA-3213
title: "Share Toggle Shows a Per-Row Pending/Loading State While Its Own Save Is In Flight"
priority: low
type: ui
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3213: Per-Row Pending/Loading State for the Share Toggle

**Module:** Secrets · **Priority:** Low · **Type:** UI

**Objective:** Confirm that when a share-toggle change is saving, only that specific row shows a pending/loading indicator (spinner, disabled-briefly, etc.) — other rows' toggles remain fully interactive, and there's no global page-level lock while one toggle saves.

**Coverage:** TC-UI (per-row pending/loading state)

## Preconditions

- At least two secrets exist in the same project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Throttle the network slightly (devtools) so the save isn't instantaneous. | Save requests take a visible moment. |
| 2 | Flip the toggle on secret row A. | Row A's toggle shows a pending/loading indicator while the request is in flight. |
| 3 | While row A's save is still pending, attempt to flip the toggle on secret row B. | Row B's toggle is fully interactive and unaffected by row A's in-flight save — no global lock. |
| 4 | Wait for row A's save to complete. | Row A's pending indicator clears and reflects the new persisted state. |

## Expected Final State

Pending state is scoped per-row; concurrent independent toggles on different secrets don't block each other.

## Pass/Fail Criteria

**Pass:**
- Pending indicator is isolated to the row being saved; other rows remain interactive throughout

**Fail:**
- The whole page/table locks while one toggle saves
- No pending indicator at all, risking duplicate rapid clicks/double-submits
