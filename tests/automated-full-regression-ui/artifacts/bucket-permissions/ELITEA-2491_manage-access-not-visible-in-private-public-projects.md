---
id: ELITEA-2491
title: "Manage Access Not Visible in Private and Public Projects"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---

# ELITEA-2491: Manage Access Not Visible in Private and Public Projects

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that the "Manage access" option is NOT available in Private and Public projects — only in Team projects.

---

## Preconditions

- User is logged in to the Elitea platform
- User has access to a Private project with at least one bucket
- User has access to a Public project with at least one bucket
- User has access to a Team project with at least one bucket

---

## Test Data

| Field | Value |
|-------|-------|
| Team project | Bugs & Features (or similar Team project) |
| Private project | Any Private project with buckets |
| Public project | Any Public project with buckets |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login to the platform | Login successful |
| 2 | Navigate to a Team project | Project opens |
| 3 | Go to Artifacts and select any bucket | Bucket selected |
| 4 | Click context menu (3 dots) next to bucket name | Context menu opens |
| 5 | Verify "Manage access" option IS present | "Manage access" visible in Team project |
| 6 | Close context menu | Menu closes |
| 7 | Navigate to a Private project | Project opens |
| 8 | Go to Artifacts and select any bucket | Bucket selected |
| 9 | Click context menu (3 dots) next to bucket name | Context menu opens |
| 10 | Verify "Manage access" option is NOT present | "Manage access" NOT visible in Private project |
| 11 | Close context menu | Menu closes |
| 12 | Navigate to a Public project | Project opens |
| 13 | Go to Artifacts and select any bucket | Bucket selected |
| 14 | Click context menu (3 dots) next to bucket name | Context menu opens |
| 15 | Verify "Manage access" option is NOT present | "Manage access" NOT visible in Public project |

---

## Expected Final State

"Manage access" option is available only in Team projects. It is not shown in Private or Public projects.

---

## Pass/Fail Criteria

**Pass:**
- "Manage access" is present in Team project context menu
- "Manage access" is absent in Private project context menu
- "Manage access" is absent in Public project context menu

**Fail:**
- "Manage access" missing in Team project
- "Manage access" appears in Private project
- "Manage access" appears in Public project
