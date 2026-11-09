---
id: ELITEA-4535
title: "Verify toolkit overflow menu actions (Export, Fork, Copy link, Pin to top, Delete) behave correctly without leaking the credential"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid credential, saved

## Test Data

| Action | Target |
|--------|--------|
| Export | The saved toolkit |
| Fork | The saved toolkit |
| Copy link | The saved toolkit |
| Pin to top | The saved toolkit |
| Delete | A disposable test toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the overflow menu | Lists Export, Fork, Copy link, Pin to top, Delete |
| 2 | Click "Export" and inspect the exported content | Contains the credential reference (`configuration_uuid`, etc.) but never the literal API key value |
| 3 | Click "Fork" and open the forked copy | A new toolkit copy is created; document whether it retains the credential reference, requires re-selecting a credential, or is left credential-invalid |
| 4 | Click "Copy link" and open the copied URL in a new tab/session with access | Opens this same Tavily toolkit |
| 5 | Click "Pin to top", then unpin | Toolkit is pinned/highlighted, then returns to normal ordering |
| 6 | Click "Delete" on a disposable test toolkit | A confirmation prompt appears before removal |

## Expected Final State

All overflow menu actions behave correctly and never expose the literal API key.

## Pass/Fail Criteria

**Pass:**
- Every action behaves as expected
- Export never contains the literal key

**Fail:**
- Any action misbehaves
- Export/Fork exposes the literal API key value
