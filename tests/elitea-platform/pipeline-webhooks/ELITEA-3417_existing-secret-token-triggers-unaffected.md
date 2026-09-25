---
id: ELITEA-3417
title: "Existing Secret Token GitLab Triggers Keep Working Unmodified"
priority: high
type: functional
module: webhooks
status: draft
execution_type: manual
tags: [feat:pipelines, int:gitlab, story:5097, webhooks, regression]
requirements: [EliteaAI/elitea_issues#5097]
---
# ELITEA-3417: Existing Secret Token Triggers Keep Working Unmodified

**Module:** Webhooks · **Priority:** High · **Type:** Functional

**Objective:** Confirm backward compatibility — a GitLab webhook trigger created before this feature shipped (no `gitlab_auth_method` set) keeps validating deliveries via the legacy `X-Gitlab-Token` header exactly as before, with no migration step required.

**Coverage:** AC — backward compatibility maintained for existing webhook configurations

## Preconditions

- A GitLab pipeline webhook trigger that existed prior to this feature (or one manually left at the default auth method, with no signing token ever configured)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the trigger's webhook settings in the UI. | Auth method shows as "Secret token" (the default), with no signing-token configuration present. |
| 2 | Send a real or replayed GitLab delivery with a valid `X-Gitlab-Token` header matching the configured secret. | Request is accepted; pipeline runs, exactly as before this feature existed. |
| 3 | Send the same delivery with an incorrect `X-Gitlab-Token` value. | Request is rejected, as before. |

## Expected Final State

Pre-existing secret-token triggers continue to validate on `X-Gitlab-Token` alone, unaffected by the new signing-token option.

## Pass/Fail Criteria

**Pass:**
- Valid `X-Gitlab-Token` delivery is accepted and invalid one is rejected, identical to pre-feature behavior

**Fail:**
- Existing trigger behaves differently than before (e.g. now requires a signing header, or fails validation it previously passed)
