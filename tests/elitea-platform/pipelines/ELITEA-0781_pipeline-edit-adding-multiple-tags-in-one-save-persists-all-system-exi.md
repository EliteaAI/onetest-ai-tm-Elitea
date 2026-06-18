---
id: ELITEA-0781
title: "[Pipeline Edit] Adding Multiple Tags in One Save Persists All — System-Existing and Mixed [Parametrized]"
priority: high
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [bug-env:next, feat:tags, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5151]
---
# ELITEA-0781: [Pipeline Edit] Adding Multiple Tags in One Save Persists All — System-Existing and Mixed [Parametrized]

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that adding multiple tags in a single save operation persists all of them on pipelines, covering both the all-system-existing scenario and a mixed scenario (system-existing + system-new).

**Coverage:**
- Variant A: All tags are system-existing (already used by other agents or pipelines)
- Variant B: Mix of system-existing and system-new tags in the same save
- Confirms behavior is consistent for pipelines regardless of tag origin
- All tags survive hard page reload

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- An existing pipeline with no tags is available
- Identify at least 3 tags already in use by other agents or pipelines in the system (system-existing)
- Prepare 2 tag values that have never been used anywhere in the system (system-new) — for Variant B only
- Browser: Chrome latest

## Test Data

**Variant A — All system-existing tags:**
- Tags to add: ExistingSystemTag1 (system-existing), ExistingSystemTag2 (system-existing), ExistingSystemTag3 (system-existing)

**Variant B — Mixed tags:**
- Tags to add: ExistingSystemTag1 (system-existing), ExistingSystemTag2 (system-existing), BrandNewPipeTag_Mix1 (system-new), BrandNewPipeTag_Mix2 (system-new)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines and open an existing pipeline with no tags. | Pipeline edit view opens; tag field is empty. |
| 2 | **[Variant A]** Add ExistingSystemTag1, ExistingSystemTag2, ExistingSystemTag3. **[Variant B]** Add ExistingSystemTag1, ExistingSystemTag2, BrandNewPipeTag_Mix1, BrandNewPipeTag_Mix2. | All tag chips appear (Variant A: 3 chips; Variant B: 4 chips). |
| 3 | Click Save. | Save completes with no error. |
| 4 | Hard-reload the page and reopen the same pipeline. | Pipeline detail view loads from fresh state. |
| 5 | Inspect the tag field. | **[Variant A]** All 3 system-existing tags present. **[Variant B]** All 4 tags (both system-existing and both system-new) present. |

## Expected Final State

**[Variant A]** All 3 system-existing tags present. **[Variant B]** All 4 tags (both system-existing and both system-new) present.

## Pass/Fail Criteria

**Pass:**
- All tags from the chosen variant are present after save and hard reload

**Fail:**
- Any tag missing — particularly system-new tags in Variant B
