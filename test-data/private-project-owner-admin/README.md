# Test data: private-project owners hold project Admin (#7507)

Used by `tests/elitea-platform/settings/private-project-owner-admin/` (ELITEA-4983 to ELITEA-4996, manual) and `tests/automated-full-regression-ui/settings/private-project-owner-admin/` (ELITEA-4997 to ELITEA-5001, UI regression).

Implementation: admin#83 (`_owner_only_admin` guard), projects#20 (new private projects give the owner admin+editor+viewer), auth_core#38 (migration grants admin to verified owners of existing private projects).

## Accounts

| Account | Setup |
|---|---|
| **User A** (owner) | Owner of a private project **P-A**; Admin of a team project **T** |
| **User B** | Another user: owner of their own private project **P-B**. At the start and end of every case B is **not** a member of P-A or T |

- User A should **not** be a platform admin, or the platform checks can't fail (run those as User B).
- A private project has no Settings → Users page (it redirects to General). Read memberships through the API below, or use the "Teammates: N" count on General.
- Each user's API calls run in that user's own browser session (DevTools console `fetch`, or an API client with that user's token).

## API calls (`{{base_url}}/api/v2/...`)

| Purpose | Call |
|---|---|
| Members and roles | `GET admin/users/default/{project_id}` |
| Add a member | `POST admin/users/default/{project_id}` `{"emails": ["<email>"], "roles": [...]}` |
| Change a member's roles | `PUT admin/users/default/{project_id}` `{"id": <user_id>, "roles": [...]}` |
| Remove a member | `DELETE admin/users/default/{project_id}?id[]=<user_id>` |
| Effective permissions | `GET auth/permissions/prompt_lib/{project_id}` |
| Settings flag | `GET elitea_core/project_info/prompt_lib/{project_id}/project-info` → `can_manage_settings` |
| Backup summary | `GET admin/project_backup_summary/prompt_lib/{project_id}` |

## Non-destructive authorization probes

Each probe fails validation *after* the authorization check, so an authorized caller gets a 400 and nothing changes. A denied caller gets 403.

| Feature | Probe | Authorized | Denied |
|---|---|---|---|
| Delete Project Data | `GET admin/project_data_delete/prompt_lib/{project_id}`, then `POST` the same path with `{"types": []}` | GET 200, POST 400 "types must be a non-empty list" | 403 `access_denied` on both |
| Restore from the Backup | `POST admin/project_restore/prompt_lib/{project_id}` with no file | 400 "no file provided" | 403 `access_denied` |
| Schedule settings (`schedules.admin`) | `PUT elitea_core/schedules/prompt_lib/{project_id}/settings` `{"qa_probe": true}` | 400 with `field: qa_probe`, nothing saved | 403 |
| Users management | `POST admin/users/default/{project_id}` `{"emails": ["qa-not-an-email"], "roles": ["viewer"]}` | 400 per-item validation error, nobody added | 403 |

Never send a real delete or restore request on a shared project.

## Admin-only permissions

An owner of a private project and a team Admin hold all of these. An Editor or Viewer holds none:

`models.project_data.delete`, `models.project_backup.restore`, `models.applications.schedules.admin`, `configuration.users.users.create`, `configuration.users.users.edit`, `configuration.users.users.delete`, `credentials.manage`, `governance.bindings.manage`, `governance.mandates.manage`, `projects.projects.project.edit`

**Not admin-only:** `models.project_backup` / `models.project_backup.download`. Downloading a backup is a member action for Editors by design (admin `module.py`). Viewers are excluded, and Restore stays admin-only.
