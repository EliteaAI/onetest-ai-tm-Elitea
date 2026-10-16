---
id: ELITEA-4085
title: "Custom logo upload replaces default Elitea logo in sidebar for Project theme users"
priority: high
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, logo, branding]
requirements: []
---

# ELITEA-4085: Custom logo upload replaces default Elitea logo in sidebar for Project theme users

**Module:** admin-portal/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that administrators can upload a custom platform logo and it replaces the default Elitea logo in the sidebar for all users who select the Project theme.

---

## Preconditions

- User has Admin role with access to Admin Portal
- Have a valid test logo file ready:
  - Format: PNG or SVG
  - Size: Under 5MB
  - Transparent background recommended
  - Visually distinct from default Elitea logo
- Second user account available for verification

---

## Test Data

| Field | Value |
|-------|-------|
| Logo file format | PNG or SVG |
| Max file size | 5MB |
| Test logo | Custom branded logo (visually distinct) |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log into Admin Portal as admin user | Admin Portal dashboard loads |
| 2 | Navigate to Features → Custom Theme | Custom Theme configuration page loads |
| 3 | Locate "Platform Logo" section (shows "1 setting") | Platform Logo section is visible with upload area |
| 4 | Verify upload area shows instruction text | Text displays: "Upload a custom logo to replace the default Elitea logo in the sidebar, chat header, and favicon" |
| 5 | Verify accepted formats message | Message shows: "PNG, SVG · Max 5MB" |
| 6 | Drag and drop valid PNG/SVG logo file onto upload area | Upload area highlights during drag; file uploads |
| 7 | Observe upload progress | Progress indicator shows upload status |
| 8 | Verify logo preview displays after upload | Uploaded logo appears in preview area |
| 9 | Click "Save Changes" button | Changes are saved successfully |
| 10 | Open new browser/incognito window | New browser session starts |
| 11 | Log in as regular user (non-admin) | User lands on default page |
| 12 | Navigate to Settings > Preferences | Preferences page loads |
| 13 | Select "Project" theme | Project theme is applied |
| 14 | Observe sidebar logo | Custom uploaded logo displays instead of default Elitea logo |
| 15 | Collapse sidebar (if applicable) | Sidebar collapses |
| 16 | Verify logo displays correctly in collapsed state | Logo maintains aspect ratio and visibility |

---

## Expected Final State

Custom logo uploaded by admin replaces default Elitea logo in sidebar for all users who have Project theme selected, in both expanded and collapsed sidebar states.

---

## Pass/Fail Criteria

**Pass:**
- Logo upload via drag-drop works correctly
- Accepted file types (PNG, SVG) upload successfully
- Files over 5MB are rejected with appropriate error
- Logo preview displays after upload
- Custom logo appears for users on Project theme
- Logo displays correctly in both sidebar states

**Fail:**
- Upload fails for valid file types
- No preview after successful upload
- Default logo still shows for Project theme users
- Logo distorted or cropped incorrectly
- Upload accepts files over size limit
