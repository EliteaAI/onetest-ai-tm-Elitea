---
id: ELITEA-3443
title: "Automated Pipeline, Webhook, and Index Triggers Are Excluded from User Activity"
priority: high
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [feat:monitoring, feat:pipelines, int:webhooks, story:5110, regression, data-integrity]
requirements: [EliteaAI/elitea_issues#6802]
---
# ELITEA-3443: Automated Pipeline, Webhook, and Index Triggers Are Excluded from User Activity

**Module:** Settings → Analytics · **Priority:** High · **Type:** Functional

**Objective:** Confirm that automated executions — scheduled pipeline runs, webhook-triggered pipeline runs, and index runs — are not attributed to or counted as the configuring user's personal activity in the Users/Activity tabs or the Overview page's "top AI adopters" list — regression check for #6802. This is a metric-integrity bug: automated triggers inflate/misrepresent a user's actual engagement.

**Coverage:** Regression — [EliteaAI/elitea_issues#6802](https://github.com/EliteaAI/elitea_issues/issues/6802).

## Preconditions

- A project with Team Analytics enabled
- Ability to create a scheduled pipeline and a webhook-triggered pipeline/index run

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a test project, create a scheduled pipeline (or a webhook-triggered pipeline/index run) configured by a specific user. | Pipeline/schedule/webhook saves successfully. |
| 2 | Note the configuring user's current activity/"active" status on the Users and Activity tabs and the Overview "top AI adopters" list, before the automated trigger fires. | Baseline recorded. |
| 3 | Wait for the scheduled pipeline or webhook to trigger automatically (do not run it manually). | The automated run executes. |
| 4 | Return to Team Analytics → Users and Activity tabs, and the Overview "top AI adopters" list. | Compare against the step-2 baseline. |
| 5 | Separately, have the same user perform one direct manual action (e.g. send a chat message or manually run a pipeline). | The manual action succeeds. |
| 6 | Check the Users/Activity tabs again. | The manual action from step 5 *is* reflected as activity, distinguishing it from the automated trigger in step 3. |

## Expected Final State

Automated executions (scheduled pipelines, webhook triggers, index runs) never count as, or inflate, the configuring user's personal activity metrics; only direct manual actions (UI or API) do.

## Pass/Fail Criteria

**Pass:**
- Step 4 shows no change in the configuring user's activity/"active" status attributable to the automated trigger
- Step 6 confirms manual actions are still correctly counted, proving the exclusion is specific to automated triggers and not a blanket activity-tracking failure

**Fail:**
- The automated trigger in step 3 is counted as/toward the configuring user's activity in step 4
