---
id: ELITEA-3419
title: "Secret Token Strength Validation and Rotation Audit Logging"
priority: medium
type: functional
module: webhooks
status: draft
execution_type: manual
tags: [feat:pipelines, int:gitlab, story:5097, webhooks, security]
requirements: [EliteaAI/elitea_issues#5097]
---
# ELITEA-3419: Secret Token Strength Validation and Rotation Audit Logging

**Module:** Webhooks · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a user-supplied secret token is rejected when it doesn't meet minimum strength requirements, and that rotating/regenerating a webhook secret produces an audit log entry without ever recording the actual secret value.

**Coverage:** AC — secret validation enforces minimum security requirements; audit logging records rotation events without storing secret values

## Preconditions

- A pipeline with a GitLab webhook trigger set to "Secret token" method
- Access to audit/event logs for the project or trigger

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Attempt to set the secret token to a short/weak value (e.g. a few characters). | Save is rejected with a validation error about minimum length/complexity; no weak value is persisted. |
| 2 | Set the secret token to a value meeting the minimum requirements. | Save succeeds. |
| 3 | Use the regenerate/rotate action to produce a new secret. | A new secret is generated server-side and saved; success notification shown. |
| 4 | Check the audit log around the time of the rotation in step 3. | An audit event is recorded for the rotation (e.g. `PUT`/`POST` to the trigger endpoint); the raw secret value does not appear anywhere in the log entry. |

## Expected Final State

Weak secrets are rejected, and every rotation is auditable without ever exposing the secret value in logs.

## Pass/Fail Criteria

**Pass:**
- Weak secret token is rejected
- Rotation is recorded in the audit log with no secret value present in the entry

**Fail:**
- A weak/short secret is accepted
- Rotation produces no audit entry, or the entry contains the raw secret value
