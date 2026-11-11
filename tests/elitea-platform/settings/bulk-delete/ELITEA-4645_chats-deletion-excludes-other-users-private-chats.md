---
id: ELITEA-4645
title: "Chats deletion excludes other users' private chats"
priority: high
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Team project; Admin's own chats exist; another user has at least one private chat not visible to Admin

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Admin account | team-admin@test |
| Other user account | team-member@test |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Admin, note the Chats count shown in Delete Project Data | Count recorded |
| 2 | As the other user, confirm their private chat exists and is accessible to them | Private chat accessible |
| 3 | As Admin, select Chats only and complete the deletion | Deletion completes |
| 4 | As Admin, check the Chats list | All chats visible to Admin are removed; count resets |
| 5 | Log back in as the other user and check their private chat | Private chat still exists and is unaffected |

## Expected Final State

Admin's visible chats are deleted; the other user's private chat (not visible to Admin) survives untouched.

## Pass/Fail Criteria

**Pass:**
- Other user's private chat unaffected

**Fail:**
- Other user's private chat is deleted or altered
