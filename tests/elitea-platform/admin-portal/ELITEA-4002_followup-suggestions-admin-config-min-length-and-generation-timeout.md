---
id: ELITEA-4002
title: "Admin Portal – Follow-Up Suggestions Minimum-Length Threshold and Generation-Timeout (Default 15s) Configs Are Respected"
priority: high
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-portal, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-4002: Admin Portal – Follow-Up Suggestions Minimum-Length Threshold and Generation-Timeout (Default 15s) Configs Are Respected

**Module:** admin-portal · **Priority:** High · **Type:** Functional

**Objective:** Verify Admin Portal's configurable minimum character/length threshold for suggestion eligibility, and its generation-timeout setting (default 15 seconds), both take effect correctly and predictably.

---

## Preconditions

- Admin has access to the Admin Portal follow-up suggestions configuration section.
- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Ability to simulate a deliberately slow suggestion backend for timeout testing.

---

## Test Data

| Field | Value |
|-------|-------|
| Threshold value A | Lower than default (makes previously too-short replies eligible) |
| Threshold value B | Higher than default (makes previously-eligible replies skipped) |
| Timeout value | Lowered to 1–2 seconds against a deliberately slow suggestion backend |
| Timeout value (raised) | Raised above the default 15s |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | In Admin Portal, lower the minimum-length threshold to Threshold value A | A previously too-short AI reply (below the old default, above the new lower value) now becomes suggestion-eligible for new responses |
| 2 | Raise the minimum-length threshold to Threshold value B | A previously-eligible reply length now becomes ineligible for new responses |
| 3 | Confirm the changed threshold takes effect for new AI responses without requiring logout/reload (or note if a reload is required and confirm that is documented/expected) | Threshold change is observed to take effect per the app's actual behavior |
| 4 | Set the generation timeout to Timeout value (1–2s) against the slow suggestion backend, then send a suggestion-eligible message | The suggestion call is aborted at roughly the configured window (not the old 15s default); no chip list, no error |
| 5 | Set the generation timeout to Timeout value (raised) and send a suggestion-eligible message against a backend that responds slowly but within the new timeout | Suggestion chips render successfully once the response lands, provided the user has not already sent/typed a new message in the meantime |

---

## Expected Final State

Both the minimum-length threshold and the generation-timeout config are enforced according to their currently configured values, not hardcoded defaults.

---

## Pass/Fail Criteria

**Pass:**
- Threshold boundary moves correctly with the configured value in both directions.
- Timeout aborts a slow suggestion call at roughly the configured window, silently.
- A raised timeout allows a slow-but-successful suggestion response to still render, subject to the standard lifecycle-clearing rules.

**Fail:**
- Threshold changes have no effect, or the boundary does not move with the configured value.
- Timeout is not respected (call is aborted too early/late relative to configuration).
- A successful-but-slow suggestion within a raised timeout fails to render, or renders after the user has already moved on (violating lifecycle rules).
