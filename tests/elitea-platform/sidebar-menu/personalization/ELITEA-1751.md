---
id: ELITEA-1751
title: "Verify QA, Nerdy, Quirky, Cynical personalities unchanged"
priority: critical
type: regression
module: personalization
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, regression, backwards-compatibility, qa-persona, nerdy-persona, quirky-persona, cynical-persona]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1751: Verify QA, Nerdy, Quirky, Cynical personalities unchanged

**Module:** Personalization · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that QA, Nerdy, Quirky, and Cynical personalities remain unchanged after Bare personality addition

## Preconditions

- User is logged into EliteA platform
- User has baseline knowledge of QA, Nerdy, Quirky, Cynical personality behaviors
- User can create multiple conversations
- All personalities available in personality dropdown

## Test Data

- Test prompt (used for all personalities): "What is artificial intelligence?"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation for QA personality | New conversation opens |
| 2 | Select "QA" personality via Context Management | QA personality selected |
| 3 | Send message: "What is artificial intelligence?" | Response has QA characteristics: Q&A format, structured |
| 4 | Verify QA behavior matches baseline | Response format and style unchanged |
| 5 | Create new conversation for Nerdy personality | New conversation opens |
| 6 | Select "Nerdy" personality via Context Management | Nerdy personality selected |
| 7 | Send message: "What is artificial intelligence?" | Response has Nerdy characteristics: technical, detailed, enthusiastic |
| 8 | Verify Nerdy behavior matches baseline | Response format and style unchanged |
| 9 | Create new conversation for Quirky personality | New conversation opens |
| 10 | Select "Quirky" personality via Context Management | Quirky personality selected |
| 11 | Send message: "What is artificial intelligence?" | Response has Quirky characteristics: playful, creative, unconventional |
| 12 | Verify Quirky behavior matches baseline | Response format and style unchanged |
| 13 | Create new conversation for Cynical personality | New conversation opens |
| 14 | Select "Cynical" personality via Context Management | Cynical personality selected |
| 15 | Send message: "What is artificial intelligence?" | Response has Cynical characteristics: skeptical, critical, realistic |
| 16 | Verify Cynical behavior matches baseline | Response format and style unchanged |
| 17 | Compare all responses with pre-Bare-feature baseline | All behaviors match historical baselines |

## Expected Final State

- QA personality unchanged: structured Q&A format
- Nerdy personality unchanged: technical and enthusiastic
- Quirky personality unchanged: playful and creative
- Cynical personality unchanged: skeptical and critical
- No regression in any existing personality
- All personalities work independently of Bare addition

## Pass/Fail Criteria

**Pass:**
- All four personalities behave as expected
- Each personality maintains unique characteristics
- Behaviors match pre-Bare baselines
- No degradation in response quality
- No unintended side effects from Bare addition

**Fail:**
- Any personality behavior changed unexpectedly
- Personality characteristics lost or diluted
- Behaviors don't match baseline
- Response quality degraded
- New bugs affecting existing personalities
