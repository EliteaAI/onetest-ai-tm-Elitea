---
id: ELITEA-2485
title: "Settings personality change affects NEW conversations only"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2485: Settings personality change affects NEW conversations only

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Settings changes don't affect existing conversations

## Preconditions

- Existing Chat conversation, Settings shows "Generic"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send message in existing conversation: "Explain APIs" | |
| 2 | Note Generic personality response | |
| 3 | Change Settings to "Nerdy" | |
| 4 | Return to SAME conversation, send "Explain APIs" | |
| 5 | Note response still uses Generic | |
| 6 | Create NEW conversation, send "Explain APIs" | |
| 7 | Note response now uses Nerdy personality | |

## Expected Results

- Existing conversation maintains Generic personality
- New conversation uses Nerdy personality
- Settings affect NEW conversations only

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
