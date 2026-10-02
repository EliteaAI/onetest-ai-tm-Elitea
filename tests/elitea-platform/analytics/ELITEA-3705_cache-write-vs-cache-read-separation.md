---
id: ELITEA-3705
title: "Verify Cache Write Populates Only on First Call and Cache Read Only on Repeat Call"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6705]
---

# ELITEA-3705: Verify Cache Write Populates Only on First Call and Cache Read Only on Repeat Call

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify cache write cost/tokens populate only on the call that establishes the cache, and cache read cost/tokens populate only on a subsequent call that reuses it.

**Coverage:**
- Cache Write > 0 / Cache Read ≈ 0 on first call
- Cache Read > 0 / Cache Write ≈ 0 on repeat call

## Preconditions

- Access to Settings > Analytics > Costs/Tokens
- A caching-capable platform-managed model available as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| Model | Bedrock-GPT-5.6-Luna (or equivalent caching-capable model) |
| First message | A long cacheable prompt/context (≥1024 tokens) |
| Second message | A follow-up reusing the exact same cached prefix |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a chat with the caching-capable model and send the first message | Model responds |
| 2 | Open Analytics > Costs/Tokens for this call | Cache Write cost/tokens > 0; Cache Read cost/tokens ≈ 0 |
| 3 | In the same conversation, send the second message reusing the same cached prefix | Model responds |
| 4 | Open Analytics > Costs/Tokens for this second call | Cache Read cost/tokens > 0; Cache Write cost/tokens ≈ 0 |

## Expected Final State

Cache Write is populated only on the call establishing the cache; Cache Read is populated only on the call reusing it.

## Pass/Fail Criteria

**Pass:**
- First call: Cache Write > 0, Cache Read ≈ 0. Second call: Cache Read > 0, Cache Write ≈ 0

**Fail:**
- Either call shows both non-zero, or shows the wrong metric populated
