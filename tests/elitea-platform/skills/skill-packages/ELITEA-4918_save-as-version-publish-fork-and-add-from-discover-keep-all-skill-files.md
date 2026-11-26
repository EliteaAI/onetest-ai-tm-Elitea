---
id: ELITEA-4918
title: "Save As Version, publish, fork and adding from Discover keep all skill files"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, feat:publishing, feat:fork, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7185]
---

# ELITEA-4918: Save As Version, publish, fork and adding from Discover keep all skill files

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that saving a skill as a new version, publishing it, forking it and adding it to an agent from Discover keep all of its files.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in Project A and Project B.
- Skill `qa-7185-pkg` is in Project A and shows **Files – 2** (see ELITEA-4916).
- Agent G exists in Project B.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill | `qa-7185-pkg` |
| Version name | `v2` |
| Target project | Project B |
| Agent | G |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **Save As Version**, enter `v2` in **Create version**, click **Save** | Version `v2` opens with **Files – 2** |
| 2 | Open ⋮ → **Publish** and complete the **Publish version** wizard (Version name, Category, Publishing Terms) | The skill is published |
| 3 | Open Skills → **Discover**, open the published skill, then ⋮ → **Export** | The ZIP contains all the files |
| 4 | In the Discover preview open ⋮ → **Fork**, choose Project B in **Fork parameters**, click **Fork**, then **Got it** | **Fork Complete** lists the skill. The fork opens in Project B with **Files – 2** |
| 5 | In the Discover preview click **Add to Agent** and choose agent G | The skill attached to G has all the files (its Files card shows the same counts) |

---

## Expected Final State

Every copy of the skill has the same two files. Unpublish and delete the test entities after the run.

---

## Pass/Fail Criteria

**Pass:**
- The file list is identical in every copy.

**Fail:**
- A file is missing in any version, published copy, fork or added copy.

---

## Notes

- The Discover preview and the **Fork parameters** dialog show no file list. Check files on the skill page or in an export.
- Same flows as ELITEA-2595, ELITEA-2602 and ELITEA-4766, now checking files.
