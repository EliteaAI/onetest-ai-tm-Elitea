---
id: ELITEA-4190
title: "Verify skill execution respects configured reasoning effort setting"
priority: critical
type: functional
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill with reasoning model and reasoning level configured exists (e.g., Medium or High)
- User has permission to run skills

## Test Data

| Field | Value |
|-------|-------|
| Model | Claude Opus (5-point reasoning) |
| Reasoning level | High |
| Test prompt | "Explain quantum computing in simple terms" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with reasoning level set to "High" | Skill details page opens |
| 2 | Verify "Run settings" → Model settings shows Reasoning: High | Reasoning: High |
| 3 | Run skill with test prompt | Skill execution starts |
| 4 | Monitor execution time (High reasoning should take longer) | Execution in progress |
| 5 | Wait for completion | Skill run completes |
| 6 | Check API response for reasoning effort applied | Response metadata includes `reasoning_effort: "high"` or equivalent |
| 7 | Observe response quality (High reasoning should produce more thoughtful output) | Response shows deeper reasoning |
| 8 | Verify token usage reflects reasoning effort (higher token count for reasoning) | Token usage includes reasoning tokens |
| 9 | Navigate to Run History → Verify run record shows reasoning setting | Run history displays: Reasoning: High |

## Expected Final State

- Execution applies configured reasoning effort (High)
- API response confirms reasoning level used
- Token usage reflects reasoning computation
- Run history shows correct reasoning setting

## Pass/Fail Criteria

**Pass:**
- Reasoning effort "High" is applied during execution
- API response metadata confirms reasoning level
- Token usage includes reasoning tokens
- Response quality reflects higher reasoning

**Fail:**
- Reasoning effort not applied
- Execution uses default reasoning level
- No reasoning metadata in response
- Token usage does not reflect reasoning computation
