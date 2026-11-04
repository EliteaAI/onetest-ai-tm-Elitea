---
id: ELITEA-4248
title: Can create multiple chats with same Catalog skill
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, catalog, chat, multiple-instances, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4248: Can create multiple chats with same Catalog skill

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that user can create multiple independent chats with the same Catalog skill participant.

**Coverage:**
- Multiple chats can be created with same skill
- Each chat is independent
- Messages don't cross-contaminate
- All chats appear in Chats list

## Preconditions

- User is logged in to {{base_url}}
- Catalog has published skill (e.g., "animal-joke")
- User can create multiple chats

## Test Data

- Catalog skill: "animal-joke"
- Chat 1 message: "Tell me a joke about crows"
- Chat 2 message: "Tell me a joke about elephants"
- Expected: Two separate independent chats

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Catalog → Skills tab | Catalog Skills view displays |
| 2 | Click Run on "animal-joke" skill | Chat 1 is created with skill participant |
| 3 | In Chat 1, send message: "Tell me a joke about crows" | Message sent, skill responds with crow joke |
| 4 | Note the Chat 1 name/ID in Chats list | Chat 1 appears in Chats list |
| 5 | Navigate back to Catalog → Skills tab | Catalog view reopens |
| 6 | Click Run on the SAME "animal-joke" skill again | Chat 2 is created (separate from Chat 1) |
| 7 | In Chat 2, send message: "Tell me a joke about elephants" | Message sent, skill responds with elephant joke |
| 8 | Check Chats list in left sidebar | Both Chat 1 and Chat 2 appear in the list |
| 9 | Click on Chat 1 to open it | Chat 1 opens showing crow joke conversation |
| 10 | Click on Chat 2 to open it | Chat 2 opens showing elephant joke conversation |
| 11 | Verify Chat 1 has no elephant messages | Chat 1 contains only crow joke (no cross-contamination) |
| 12 | Verify Chat 2 has no crow messages | Chat 2 contains only elephant joke (no cross-contamination) |
| 13 | Verify both chats have same skill participant | Both show "animal-joke" skill in SKILLS section |

## Expected Final State

Two separate independent chats created with same skill; no cross-contamination; both in Chats list.

## Pass/Fail Criteria

**Pass:** Two chats created successfully, each is independent, messages don't mix, both appear in Chats list.

**Fail:** Cannot create second chat, messages cross-contaminate, or chats are not independent.
