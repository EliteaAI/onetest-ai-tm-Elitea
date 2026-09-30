---
id: ELITEA-3498
title: "Display Name Consistency Across Analytics"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3498: Display Name Consistency Across Analytics

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify model Display Names are shown consistently (never raw model identifiers).

## Preconditions

- Logged into {{base_url}}
- Project has models with configured Display Names
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Analytics → Overview tab. | Locate Model Usage Breakdown table. |
| 2 | Verify MODEL column shows friendly names. | Names like "Bedrock-GPT-5.6-Luna" not raw IDs. |
| 3 | Open Analytics → Costs tab. | Locate Cost by Model table. |
| 4 | Verify MODEL column matches Overview naming. | Same friendly names displayed. |
| 5 | Open Analytics → Tokens tab. | Locate Token Usage by Model table. |
| 6 | Verify MODEL column consistent. | Same friendly names as other tabs. |
| 7 | Check for any raw model identifiers. | No entries like "openai/gpt-4", "anthropic/claude-3", "123_model-name". |
| 8 | If external PAT usage exists, verify fallback. | External models show raw name if Display Name not resolvable (acceptable). |

## Pass/Fail Criteria

**Pass:** All configured models show Display Names consistently across all tabs.
**Fail:** Raw model identifiers shown for models with configured Display Names.
