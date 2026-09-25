---
id: ELITEA-3418
title: "Webhook Settings UI: Auth Method Selection, Labels, and Dynamic Example"
priority: medium
type: functional
module: webhooks
status: draft
execution_type: manual
tags: [feat:pipelines, int:gitlab, story:5097, webhooks, ui]
requirements: [EliteaAI/elitea_issues#5097]
---
# ELITEA-3418: Webhook Settings UI — Auth Method Selection and Labels

**Module:** Webhooks · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the pipeline webhook settings modal, for a GitLab trigger, lets the user choose between "Secret token" and "Signing token", shows GitLab's own recommendation labeling, and updates the example request snippet to match the selected method. Also confirm the signing-token field behaves as a paste-in (GitLab-generated) value rather than an Elitea-generated/regenerable one.

**Coverage:** AC (FE) — auth method selector, recommended/not-recommended labels, dynamic example snippet, masked value with show/hide + copy

## Preconditions

- A pipeline with a GitLab webhook trigger

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the webhook settings modal for the GitLab trigger. | Two options are shown: "Signing token" and "Secret token", labeled "(recommended)" and "(not recommended)" respectively. |
| 2 | Select "Secret token". | The existing generate/regenerate flow is shown (Elitea-generated value, masked, show/hide toggle, copy button); the example request snippet shows `X-Gitlab-Token`. |
| 3 | Select "Signing token". | UI now shows a paste-in input for the GitLab-generated token (no "regenerate" button generating a new value on Elitea's side); the example request snippet updates to show `webhook-signature` (and `webhook-id`/`webhook-timestamp`) instead of `X-Gitlab-Token`. |
| 4 | Paste in a validly formatted signing token (`whsec_` prefix + base64 remainder) and save. | Success notification is shown; value is stored and displayed masked with show/hide + copy. |
| 5 | Paste in a malformed value (e.g. missing `whsec_` prefix, or invalid base64) and attempt to save. | Save is rejected with a validation error; no malformed value is persisted. |

## Expected Final State

The UI clearly distinguishes the two methods, matches GitLab's own recommendation language, and the signing-token field is presented as user-supplied rather than system-generated.

## Pass/Fail Criteria

**Pass:**
- Both methods selectable with correct recommendation labels
- Example snippet updates per selected method
- Valid signing token saves successfully; malformed one is rejected client/server-side

**Fail:**
- Recommendation labels missing or reversed
- Example snippet does not change with selection
- A malformed signing token is accepted and saved
