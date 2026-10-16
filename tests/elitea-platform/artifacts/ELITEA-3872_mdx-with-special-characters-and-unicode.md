---
id: ELITEA-3872
title: "MDX with Special Characters and Unicode"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3872: MDX with Special Characters and Unicode

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify MDX with special characters displays properly

## Preconditions

- MDX file contains special characters: é, ñ, ü, ™, ©, ®, emojis, etc.

## Test Data

- Special characters: é, ñ, ü, ™, ©, ®
- Emojis: 😀, 👍, ✅

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or locate MDX with special characters and emojis | File ready |
| 2 | Open in Preview mode | File opens |
| 3 | Observe character rendering | Characters display |
| 4 | Switch to Raw mode | Mode switches |
| 5 | Edit and save | Save completes |
| 6 | Verify characters preserved | Characters intact |

## Expected Results

- Special characters display correctly in Preview mode
- UTF-8 encoding is properly handled
- Emojis render correctly
- Characters don't appear as garbled text
- Raw mode shows correct character representation
- Editing preserves special characters after save

## Pass/Fail Criteria

**Pass:**
- All special characters display correctly
- UTF-8 encoding works properly
- Characters preserved after editing

**Fail:**
- Characters appear garbled
- Encoding issues
- Characters lost after save
