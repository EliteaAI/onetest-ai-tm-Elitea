---
id: ELITEA-2505
title: "Tiff images are handled with 64x64 dimension override"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- TIFF image file with non-64×64 dimensions prepared

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| TIFF File | `.tiff` image, 128×128 px, under 500 KB |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Prepare a TIFF image file with dimensions 128×128 | File ready |
| 2 | Open SelectIconDialog from a Skill form | Dialog opens |
| 3 | Upload the TIFF file | Upload succeeds without error |
| 4 | Inspect the resulting icon dimensions via network or direct URL | Icon stored/displayed at 64×64 px |
| 5 | Select the icon for a Skill and save | Icon applied to Skill |
| 6 | Verify icon displays correctly in all UI locations | Icon renders at appropriate size |

## Expected Final State

TIFF images are always handled with 64×64 dimensions due to FileReader limitations, regardless of original dimensions.

## Pass/Fail Criteria

**Pass:**
- TIFF file uploads successfully
- Stored icon is 64×64 px
- Icon displays correctly

**Fail:**
- TIFF upload fails
- Dimensions not set to 64×64
- Image corruption
