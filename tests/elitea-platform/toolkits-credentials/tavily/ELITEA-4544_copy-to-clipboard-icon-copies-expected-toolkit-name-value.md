---
id: ELITEA-4544
title: "Verify the Copy to clipboard icon next to Toolkit Name copies the expected value"
priority: medium
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A saved Tavily toolkit, open on its Configuration page

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | As currently saved |
| Renamed (unsaved) | A different, unsaved name |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click the "Copy to clipboard" icon next to Toolkit Name | Icon action completes without error |
| 2 | Paste the clipboard contents elsewhere (e.g. a chat message box) | Matches the expected value (the toolkit's name as shown in the field, or its ID if that is the intended behavior) |
| 3 | Rename the toolkit without saving, then click the icon again | Copies either the original saved name or the in-progress edited name consistently; document which |

## Expected Final State

The Copy to clipboard icon is confirmed to copy a correct, non-stale value.

## Pass/Fail Criteria

**Pass:**
- Clipboard content matches the expected value in both the saved and unsaved-edit scenarios, consistently

**Fail:**
- Clipboard content is empty, stale, or does not match either the saved or edited name as documented
