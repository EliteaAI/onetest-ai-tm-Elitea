---
id: ELITEA-4111
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Configuration Flexibility"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-4111: ADO Toolkit — Configuration Flexibility

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that `process_images` parameter is configurable at multiple levels and can be toggled flexibly.

## Preconditions

- ADO toolkit available
- Multiple toolkit instances can be configured independently
- Agent and pipeline configuration interfaces accessible

## Test Data

| Level | Scope | Example |
|-------|-------|---------|
| Instance | Per toolkit instance | Two ADO toolkits: one with true, one with false |
| Call | Per tool invocation | Toggle between calls |
| Agent | Per agent | Different agents, different settings |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure first ADO toolkit instance with `process_images: true`. | Instance A processes images. |
| 2 | Configure second ADO toolkit instance with `process_images: false`. | Instance B skips images (independent). |
| 3 | Use both instances in same agent. | Each respects its own configuration. |
| 4 | Call Instance A's get_comments: verify images processed. | Instance A includes image descriptions. |
| 5 | Call Instance B's get_comments: verify images skipped. | Instance B returns only text. |
| 6 | Reconfigure Instance B to `process_images: true`. | Configuration updated. |
| 7 | Call Instance B again: verify images now processed. | Instance B now includes images. |
| 8 | Verify default propagates to new toolkit instances. | New instances default to false. |
| 9 | Test override at agent/pipeline level (if supported). | Agent-level config can override instance default. |

## Expected Final State

- Parameter configurable per toolkit instance
- Multiple instances can have different settings
- Parameter can be toggled between calls
- Default value propagates to all new instances
- Configuration changes take effect immediately
- No conflicts between instances

## Pass/Fail Criteria

**Pass:** Per-instance config independent; toggle working; defaults propagate; level precedence correct.  
**Fail:** Config conflicts; toggle fails; wrong defaults; precedence broken.
