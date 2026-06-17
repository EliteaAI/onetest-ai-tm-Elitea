---
id: ELITEA-0166
title: "AI Validation Uses the Exact Sub-Agent Version Referenced by the Parent Agent"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4162, story:4049, story:3774]
requirements: []
---
# ELITEA-0166: AI Validation Uses the Exact Sub-Agent Version Referenced by the Parent Agent

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that AI validation evaluates the specific sub-agent version referenced by the parent agent, not the sub-agent's base or latest version.

**Coverage:**
- Validation correctly reads the pinned/referenced sub-agent version (not the base state)
- With Version 1 (empty instructions) referenced: Critical error for empty sub-agent instructions is returned
- With Version 2 (valid instructions) referenced: no Critical error for sub-agent instructions appears
- Switching the referenced sub-agent version changes the validation outcome accordingly

## Preconditions

- Logged in to ELITEA as a regular user
- Environment: {{base_url}}
- Sub-agent `VersionedSubAgent` has exactly two saved versions:
  - **Version 1:** empty instructions
  - **Version 2:** valid instructions (≥100 chars, no placeholder text)
- Parent agent `TestAgent_VersionPin` exists and can reference either version of `VersionedSubAgent`

## Test Data

- Parent agent: `TestAgent_VersionPin`
- Sub-agent: `VersionedSubAgent`
- Version 1 instructions: (empty)
- Version 2 instructions: valid (≥100 chars)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `TestAgent_VersionPin`. Configure it to reference `VersionedSubAgent` **Version 1** (empty instructions). Save the agent. | Agent saved with Version 1 referenced. |
| 2 | Click **Publish** → **Continue** on the Preparation step. Wait for validation to complete. | Validation results displayed. A Critical error appears attributed to `VersionedSubAgent` stating that sub-agent instructions are empty or missing. |
| 3 | Close the Publish modal. Return to the agent editor. Switch the sub-agent reference to `VersionedSubAgent` **Version 2** (valid instructions). Save the agent. | Agent saved with Version 2 referenced. |
| 4 | Click **Publish** → **Continue** on the Preparation step again. Wait for validation to complete. | Validation results displayed. |
| 5 | Inspect the Critical Issues section for any instruction-related error on `VersionedSubAgent`. | No Critical error about empty or missing sub-agent instructions appears. Other unrelated issues may still be present — those are acceptable. |

## Expected Final State

No Critical error about empty or missing sub-agent instructions appears. Other unrelated issues may still be present — those are acceptable.

## Pass/Fail Criteria

**Pass:**
- Step 2: Critical error for `VersionedSubAgent` empty instructions is present (confirms Version 1 was evaluated)
- Step 5: That same Critical error is absent after switching to Version 2 (confirms Version 2 was evaluated)
- Any other validation issues in Step 5 unrelated to sub-agent instructions are allowed and do not affect pass/fail

**Fail:**
- Step 2: No Critical error for empty instructions — validation did not evaluate Version 1
- Step 5: Critical error for empty instructions still appears despite Version 2 being referenced — validation read the wrong version
