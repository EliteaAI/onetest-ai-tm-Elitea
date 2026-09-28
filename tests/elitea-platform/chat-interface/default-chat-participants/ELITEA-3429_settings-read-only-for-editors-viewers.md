---
id: ELITEA-3429
title: "Default Chat Configuration Cannot Be Edited by Editors or Viewers"
priority: medium
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, feat:project-setup, feat:roles-permissions, story:6358, default-chat-config, access-control]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3429: Default Chat Configuration Cannot Be Edited by Editors or Viewers

**Module:** Chat · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that only project admins can change "Default Chat Configuration" — Editors and Viewers cannot add, remove, or save changes to the preconfigured participants list.

**Coverage:** AC — access control on the Settings UI section backing `chat_config.participants`.

## Preconditions

- A project with an existing preconfigured participants list (set by an admin)
- A user with the **Editor** role and a separate user with the **Viewer** role on the same project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as the **Editor** user and open Project Settings → "Default Chat Configuration". | Section is either not editable (read-only display) or any attempted edit/save is blocked. |
| 2 | Attempt to add or remove a participant as the Editor, then attempt Save. | Change is not persisted; no successful save occurs. |
| 3 | Log in as the **Viewer** user and repeat steps 1–2. | Same restriction applies. |
| 4 | Log back in as an **admin** and confirm the list is unchanged from before steps 1–3. | List matches the original admin-configured state — no accidental edit from the Editor/Viewer session went through. |

## Expected Final State

Only admins can modify "Default Chat Configuration"; Editors and Viewers have no way to persist a change to it, regardless of UI affordance shown.

## Pass/Fail Criteria

**Pass:**
- Editor and Viewer cannot save any change to the preconfigured participants list
- Admin's original configuration is intact afterward

**Fail:**
- An Editor or Viewer successfully saves a change to the list (add, remove, or reorder)
