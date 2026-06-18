---
id: ELITEA-0191
title: "TC-010: Version Name Must Be Unique Across All Saved Versions AND All Published Versions"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0191: TC-010: Version Name Must Be Unique Across All Saved Versions AND All Published Versions

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the publish version name is rejected if it matches any existing saved version name (e.g., "base", "v1.0") OR any already-published version name of the same agent — across both name pools simultaneously.

Coverage:
- Version name matching an existing saved version (e.g., 'base') is rejected
- Version name matching an existing published version (e.g., 'v1.0') is rejected
- Error message explicitly states the version name is already taken
- Continue button disabled while name clashes exist
- Changing to a name unique across both pools clears error and re-enables Continue

## Preconditions

- Logged in as User A
- Agent A has:
  * Saved versions: 'base' (auto-created), 'v1.0' (manually saved)
  * Published versions: 'published-v1' (already published to Studio)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent A, click 'Publish' — modal opens on the Preparation step | 'Publish version' modal opens |
| 2 | Enter 'base' in Version name field; check 'I agree with the Publishing Terms.' | Inline validation error appears (e.g., 'Version name already exists.'); Continue button remains disabled |
| 3 | Clear the field; enter 'v1.0'; checkbox remains checked | Inline validation error appears for 'v1.0'; Continue button remains disabled |
| 4 | Clear the field; enter 'published-v1'; checkbox remains checked | Inline validation error appears for 'published-v1'; Continue button remains disabled |
| 5 | Clear the field; enter 'v2.0-new'; checkbox remains checked | Error clears; Continue button becomes enabled |

## Expected Final State

Error clears; Continue button becomes enabled

## Pass/Fail Criteria

PASS:
- Names matching any existing saved version ('base', 'v1.0') are rejected with an inline error
- Names matching any existing published version ('published-v1') are rejected with an inline error
- A name unique across both pools ('v2.0-new') is accepted and enables the Continue button

FAIL:
- 'base' or any other saved version name is accepted as a publish version name
- A previously-published version name is accepted again (duplicate published version names allowed)
- No inline error shown for any of the conflicting names
- Continue button enables despite a name conflict
