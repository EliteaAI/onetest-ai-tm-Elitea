---
id: ELITEA-4641
title: "Published Agents/Skills and platform-created entities are protected from bulk deletion"
priority: critical
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Project contains at least one published Agent, one published Skill, and one platform-created credential, alongside unpublished/user-created counterparts of each type

## Test Data

| Entity Type | Protected Item | Unprotected Item |
|---|---|---|
| Agents | Published Agent | Unpublished Agent |
| Skills | Published Skill | Unpublished Skill |
| Credentials | Platform-created credential | User-created credential |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select Agents and Skills for deletion and complete the confirmation flow | Deletion completes |
| 2 | Check the Agents and Skills lists | Published Agent and published Skill still exist; unpublished Agent and Skill removed |
| 3 | Re-seed test data, select Credentials for deletion, and complete the confirmation flow | Deletion completes |
| 4 | Check the Credentials list | Platform-created credential still exists; user-created credential removed |
| 5 | Review the completion report shown after each deletion | Report accurately reflects that protected items were skipped |

## Expected Final State

Published Agents/Skills and platform-created credentials remain in the project; only unprotected, user-created/unpublished counterparts are removed.

## Pass/Fail Criteria

**Pass:**
- Protected categories survive every run
- Skips reported accurately in the completion report

**Fail:**
- A protected item is deleted
- Completion report misrepresents what was actually deleted
