---
id: ELITEA-2504
title: "Uploaded images are resized rendered at maximum 64x64 pixels"
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
- Test images of different dimensions prepared

## Test Data

| Image | Original Dimensions | Expected Stored Dimensions |
|-------|---------------------|---------------------------|
| Image A | 256×256 px | 64×64 px (resized) |
| Image B | 64×64 px | 64×64 px (unchanged) |
| Image C | 32×32 px | 32×32 or 64×64 px (per implementation) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open SelectIconDialog from a Skill form | Dialog opens |
| 2 | Upload Image A (256×256 px) | Upload succeeds |
| 3 | Inspect stored/served icon via network inspection or direct URL | Image stored at 64×64 px |
| 4 | Upload Image B (64×64 px) | Upload succeeds |
| 5 | Inspect stored/served icon | Image stored at 64×64 px |
| 6 | Upload Image C (32×32 px) | Upload succeeds |
| 7 | Inspect stored/served icon | Image dimensions handled per implementation |

## Expected Final State

Uploaded images larger than 64×64 pixels are resized to 64×64 px; images at or below 64×64 are preserved or scaled appropriately.

## Pass/Fail Criteria

**Pass:**
- Large image (256×256) resized to 64×64
- Exact size image (64×64) unchanged
- Small image handled appropriately

**Fail:**
- Large image not resized
- Image corruption during resize
- Dimensions not capped at 64×64
