---
id: ELITEA-0192
title: "TC-009: Multi-Version Publishing — Both Versions Coexist and Existing Conversations Use Correct Version"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0192: TC-009: Multi-Version Publishing — Both Versions Coexist and Existing Conversations Use Correct Version

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a second version of the same agent can be published without replacing the first, that both versions are selectable in Agents Studio, and that existing conversations on v1.0 are unaffected by the new v2.0 publication.

Coverage:
- Second publish creates a new version without overwriting v1.0
- Both v1.0 and v2.0 appear in Agents Studio
- New conversations can select either version
- Existing v1.0 conversations continue using v1.0 behavior

## Preconditions

- Agent A already has a published version 'v1.0'
- User B has an active conversation using Agent A v1.0
- Logged in as User A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Modify Agent A's instructions in the project (e.g., add 'Always respond in French') | Instructions updated and saved |
| 2 | Click 'Publish' on Agent A | Publish modal opens |
| 3 | Enter 'v2.0' in Version Name, check agreement, click Continue → validation runs → click Publish | Success notification appears; no error |
| 4 | Navigate to Agents Studio, find Agent A, check version selection | Both v1.0 and v2.0 are available as selectable versions |
| 5 | Start a new conversation selecting v2.0 | Conversation starts with v2.0 behavior (responds in French per new instruction) |
| 6 | As User B, open the existing v1.0 conversation | Conversation opens without error |
| 7 | Send a new message in User B's v1.0 conversation | Agent responds using v1.0 instructions (original language/behavior, not French) |

## Expected Final State

Agent responds using v1.0 instructions (original language/behavior, not French)

## Pass/Fail Criteria

PASS:
- Both v1.0 and v2.0 coexist in Agents Studio
- New conversations reflect v2.0 behavior when v2.0 is selected
- Existing User B v1.0 conversation uses v1.0 behavior unaffected by v2.0 publish

FAIL:
- Publishing v2.0 replaces or removes v1.0 from Studio
- Only one version appears selectable in Studio
- Existing v1.0 conversations start using v2.0 instructions after the new publish
