---
id: ELITEA-4501
title: "Paid-tool usage warning banner and limit-reached notifications for project and member scope"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4501: Paid-tool usage warning banner and limit-reached notifications for project and member scope

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Confirm that an in-chat usage banner appears while using the paid tool below its limit, and that distinct, correctly worded "limit reached" notifications appear in the Notification Center for the project-level limit and the member-level limit separately.

**Coverage:**
- In-chat banner with "View usage" link, below limit
- Member-limit-reached notification with "View my usage" link
- Project-limit-reached notification with "View project usage" link
- The two notifications are distinct, not merged or duplicated

## Preconditions

- A low, known project-level limit and a low, known member-level limit are already configured for the paid tool (e.g. Web Search) on the test project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat with Web Search enabled, trigger a paid-tool call while usage is below the limit. | Inline banner appears above the message input: "Web search: you have used X% of the project limit." with a "View usage" link; X reflects actual usage. |
| 2 | Attempt to dismiss the banner (✕) and send another message. | Banner is dismissible; sending further messages is not blocked. |
| 3 | Click "View usage". | Navigates to Settings → Usage showing the Paid Tools section. |
| 4 | Continue triggering calls as the member whose member-level limit is lower than the project limit, until that limit is reached. | Notifications Center shows: "Web search: your monthly limit of $[amount] in [project name] has been reached." with a "View my usage" link navigating to the member's own usage view. |
| 5 | Continue triggering calls (e.g. from another member, or after raising the member limit) until the project-level limit is reached. | Notifications Center shows a separate entry: "Web search: the monthly limit of $[amount] for [project name] has been reached." with a "View project usage" link navigating to the project-wide usage view. |
| 6 | Compare the two notification entries. | Member-limit-reached and project-limit-reached notifications are distinct, not merged or duplicated; each links to the correct usage scope. |

## Expected Final State

Both warning (below-limit) and limit-reached (member/project) notifications are shown correctly and distinctly, each linking to the correct usage scope.

## Pass/Fail Criteria

**Pass:**
- In-chat banner, member notification, and project notification each appear correctly worded and correctly linked

**Fail:**
- Any notification is missing, merged, duplicated, or links to the wrong usage scope
