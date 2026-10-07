---
id: ELITEA-3707
title: "Verify Cost and Tokens Are Attributed Per Participant in a Multi-Participant Conversation"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6574]
---

# ELITEA-3707: Verify Cost and Tokens Are Attributed Per Participant in a Multi-Participant Conversation

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify cost/tokens are attributed per participant/model when a conversation has two or more LLM/agent participants.

**Coverage:**
- Separate, correctly attributed entries per participant/model with no merging or dropping

## Preconditions

- Access to Analytics By User/By Model breakdowns
- Ability to add two distinct LLM or agent participants to one conversation

## Test Data

| Field | Value |
|-------|-------|
| Participant A / B | Two distinct LLM or agent participants |
| Message to A / B | "Define recursion" / "Define polymorphism" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a conversation and add Participant A and Participant B | Both participants added |
| 2 | Send the test message addressed to Participant A | Participant A responds |
| 3 | Send the test message addressed to Participant B | Participant B responds |
| 4 | Open Analytics By User and By Model breakdowns for this window | Separate, correctly attributed entries exist for each participant/model |

## Expected Final State

Each participant's cost/tokens are tracked as distinct entries, with no merging or dropping.

## Pass/Fail Criteria

**Pass:**
- Both participants show separate, correct cost/token entries

**Fail:**
- Entries are merged into one, or one participant's contribution is missing
