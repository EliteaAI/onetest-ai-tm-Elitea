---
id: ELITEA-4199
title: "Verify skill with Opus model in run_settings charges Opus cost in usage analytics, not default model"
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
- A skill with run_settings.model = Claude Opus exists
- Project default model is cheaper (e.g., GPT-4 Turbo)
- User has permission to run skills and view analytics/usage

## Test Data

| Field | Value |
|-------|-------|
| Skill model | Claude Opus (expensive) |
| Project default | GPT-4 Turbo (cheaper) |
| Test prompt | "Write a short story about AI" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with Claude Opus configured | Skill details page opens |
| 2 | Verify "Run settings" → Model: Claude Opus | Model: Claude Opus |
| 3 | Note the Claude Opus pricing (e.g., $15 per 1M input tokens, $75 per 1M output tokens) | Opus pricing noted |
| 4 | Run skill with test prompt | Skill executes |
| 5 | Wait for completion | Skill run completes |
| 6 | Navigate to Usage/Analytics dashboard or Run History | Analytics page opens |
| 7 | Find the recent skill run | Run found |
| 8 | Verify model used: Claude Opus | Model: Claude Opus |
| 9 | Verify tokens used (e.g., 500 input, 1000 output) | Token count displayed |
| 10 | Calculate expected cost: (500 × $15/1M) + (1000 × $75/1M) = $0.0825 | Expected cost: ~$0.08 |
| 11 | Verify charged cost matches Opus pricing, NOT default model pricing | Cost: $0.08 (Opus rates) |
| 12 | Verify usage_event or analytics row shows correct model_name and cost | Analytics: model=claude-opus, correct cost |

## Expected Final State

- Skill execution billed at Claude Opus rates
- Analytics shows correct model (Opus, not default)
- Token cost calculated using Opus pricing
- No incorrect billing at default model rates

## Pass/Fail Criteria

**Pass:**
- Skill charged at Claude Opus rates
- Analytics shows Claude Opus as model used
- Cost calculation matches Opus pricing
- No billing at project default model rates

**Fail:**
- Skill charged at default model rates
- Analytics shows default model instead of Opus
- Cost calculation incorrect
- Billing mismatch
