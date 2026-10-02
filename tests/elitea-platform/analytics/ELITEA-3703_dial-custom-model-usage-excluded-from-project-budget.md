---
id: ELITEA-3703
title: "Verify DIAL Custom AI Provider Model Usage Is Excluded From Platform Project Budget"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6566]
---

# ELITEA-3703: Verify DIAL Custom AI Provider Model Usage Is Excluded From Platform Project Budget

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify usage of a model configured via a user's own DIAL custom AI Provider configuration (own credentials/endpoint) is excluded from the Settings > Usage platform project-budget spend/tokens/calls, while platform-managed shared-model usage is included.

**Coverage:**
- DIAL custom-configuration call does not affect Settings > Usage figures
- Platform-managed shared-model call does affect them
- Analytics > Costs representation of the DIAL call is consistent with its budget exclusion

## Preconditions

- A DIAL AI Provider configuration using the user's own DIAL credentials/endpoint (not a platform-managed shared model) is set up in Settings > AI Providers, with a model from it available to select as a chat/agent participant
- Admin/owner access to Settings > Usage and Settings > Analytics > Costs

## Test Data

| Field | Value |
|-------|-------|
| DIAL custom model | Model configured through the user's own DIAL AI Provider configuration |
| Platform-managed model | A platform-managed shared model (e.g. Bedrock-GPT-5.6-Luna) |
| Message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record current Settings > Usage "Spent", "Tokens", "Calls" tiles and "Usage by Model" table | Baseline recorded |
| 2 | Make one call against the model configured through the custom DIAL AI Provider configuration | Response received |
| 3 | Reload Settings > Usage | Spent/Tokens/Calls tiles and "Usage by Model" table unchanged by the DIAL call |
| 4 | Make one call against a platform-managed shared model | Response received |
| 5 | Reload Settings > Usage | Spent/Tokens/Calls tiles and "Usage by Model" now increase to reflect this call |
| 6 | Open Analytics > Costs for the same window and locate the DIAL call | Record how the DIAL call is represented (e.g. shown as an estimated cost line, or excluded entirely) |
| 7 | Compare the Analytics representation against the Usage page's documented exclusion of custom-credential models | The two pages do not silently disagree |

## Expected Final State

Platform project-budget figures (Settings > Usage) increase only for platform-managed shared-model usage; DIAL custom-configuration usage never affects them, and its representation in Analytics is consistent with that exclusion.

## Pass/Fail Criteria

**Pass:**
- Usage tiles/table unchanged after the DIAL call; increased only after the platform-managed-model call

**Fail:**
- Usage tiles/table change after the DIAL call
- Analytics and Usage disagree about the DIAL call's budget treatment without explanation
