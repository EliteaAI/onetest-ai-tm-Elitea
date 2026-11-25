---
id: ELITEA-4536
title: "Verify the credential field's Open in new tab and Reload and apply changes icons work correctly"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a credential selected that is currently showing as invalid

## Test Data

| Field | Value |
|-------|-------|
| Invalid credential | Fixed to a valid API key during the test |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click "Open in new tab" next to the Tavily Configuration field | Opens that exact credential's own edit page in a new tab, not a generic credentials list |
| 2 | In the new tab, fix the API key to a valid one and save | Credential saves successfully |
| 3 | Return to the original toolkit tab and click "Reload and apply changes" | "Invalid Tavily API key" banner disappears; toolkit reflects the credential as valid, without a full page reload |
| 4 | Observe "Save" button state after the reload-and-apply action | Becomes enabled immediately, if it was previously disabled due to invalid credential |

## Expected Final State

Both icon controls are confirmed to correctly sync credential state without a full page reload.

## Pass/Fail Criteria

**Pass:**
- "Open in new tab" opens the correct credential
- "Reload and apply changes" updates validity state and Save availability without a full reload

**Fail:**
- Either icon fails to work as described
- The banner/Save state does not update correctly
