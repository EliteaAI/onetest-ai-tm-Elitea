---
id: ELITEA-4658
title: "Frontmatter name rename propagates Skill-wide via valid delimiters, then a damaged closing delimiter demotes a later edit to plain body text that does not sync or rename"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

# ELITEA-4658: Frontmatter Name Propagation vs. Damaged Delimiter Demotion

## Preconditions

- A Skill with 2 or more versions exists, each with distinct Instructions and a valid frontmatter block present
- Tester has Editor or Admin role

## Test Data

| Field | Value |
|-------|-------|
| New name (valid edit) | `renamed-skill-v2` |
| Attempted name (broken-delimiter edit) | `attempted-rename-v3` |
| Attempted description (broken-delimiter edit) | Any distinct placeholder text |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the Skill, switch to a non-base version, note current Name/Description field values for this version, and note the frontmatter values shown on at least one other version | Baseline values recorded |
| 2 | With the frontmatter block's opening and closing `---` delimiters intact, edit the `name:` value to `renamed-skill-v2` directly in the frontmatter | Edit accepted in the editor |
| 3 | Observe the Name field | Name field updates immediately to match the edited value |
| 4 | Click Save | Save completes successfully |
| 5 | Switch to a different version of the same Skill | That version's Name field and frontmatter `name` also show `renamed-skill-v2` — the rename propagated Skill-wide |
| 6 | Switch back to the originally edited version, then remove or damage the frontmatter block's closing `---` delimiter (e.g. delete the line entirely) | Frontmatter block is no longer properly delimited |
| 7 | In what is now the former `name:` line, type `attempted-rename-v3` | Text is entered in the editor |
| 8 | Observe the Name field | Name field does NOT update to `attempted-rename-v3`; it still shows `renamed-skill-v2` from step 2 |
| 9 | In what is now the former `description:` line, type the placeholder description value | Text is entered in the editor |
| 10 | Observe the Description field | Description field does NOT update to the new value; it remains at its last saved value |
| 11 | Click Save with the delimiter still missing/damaged | Save completes without error |
| 12 | Switch to the other version checked in step 5 | Its Name still reflects `renamed-skill-v2` — unaffected by the broken-delimiter edit in steps 7–10 |
| 13 | Reopen the originally edited version (navigate away and back, or switch versions and return) | A freshly regenerated, valid frontmatter block appears at the top, with `name`/`description` matching the real, persisted field values from step 2 — not the text typed in steps 7–10 |
| 14 | Inspect the body/instruction content below (or in place of) the regenerated frontmatter block | The text typed in steps 7–10 is present as plain body/instruction content, not discarded and not mistaken for frontmatter |

## Expected Final State

A genuine frontmatter edit inside intact delimiters syncs to the fields and propagates the `name` rename Skill-wide to every version. A later edit made after the closing delimiter is removed/damaged is treated as plain body text: it never syncs to the Name/Description fields, never renames the Skill, is preserved as literal body content on Save, and a clean, valid frontmatter block is regenerated from the real persisted field values on reopen.

## Pass/Fail Criteria

**Pass:**
- The valid-delimiter rename propagates to every version of the Skill
- The damaged-delimiter edit never updates the Name/Description fields and never alters the Skill's name
- Save succeeds despite the damaged delimiter, with no corruption
- Reopening shows clean, valid, regenerated frontmatter with the broken-delimiter text preserved only as body content

**Fail:**
- The valid-delimiter rename does not propagate to other versions
- The damaged-delimiter edit incorrectly updates the Name/Description fields or renames the Skill
- Save fails, errors, or corrupts the Instructions content
- Reopening shows a broken/malformed frontmatter block, or the broken-delimiter text is lost entirely
