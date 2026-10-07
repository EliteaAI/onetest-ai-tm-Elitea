---
id: ELITEA-3711
title: "Verify a Zero-Cost Custom/BYO-Provider Model Call Does Not Inflate Usage Calls/Tokens Counters"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6566]
---

# ELITEA-3711: Verify a Zero-Cost Custom/BYO-Provider Model Call Does Not Inflate Usage Calls/Tokens Counters

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify a $0 custom/BYO-model call does not inflate the Settings > Usage "Calls" or "Tokens" counters, consistent with the page's stated scope of only platform-managed shared models.

**Coverage:**
- "Calls"/"Tokens" tiles unaffected by a custom/BYO-provider model call

## Preconditions

- A model configured with the user's own provider credentials (custom/BYO, e.g. DIAL) is available as a chat participant
- Admin/owner access to Settings > Usage

## Test Data

| Field | Value |
|-------|-------|
| Custom/BYO model | Model configured with the user's own provider credentials |
| Message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings > Usage and record current "Calls" and "Tokens" tile values | Baseline recorded |
| 2 | Start a chat with the custom/BYO-provider model and send the test message | Model responds successfully |
| 3 | Reload Settings > Usage | "Calls" and "Tokens" tiles unchanged from the baseline |

## Expected Final State

Settings > Usage "Calls" and "Tokens" counters reflect only platform-managed shared-model usage, unaffected by custom/BYO-provider model calls.

## Pass/Fail Criteria

**Pass:**
- "Calls" and "Tokens" tiles remain unchanged after the custom/BYO-model call

**Fail:**
- Either tile increases after the custom/BYO-model call
