---
id: ELITEA-4805
title: "External link expiration blocks access and links are not affected by team access changes"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4805: External link expiration blocks access and links are not affected by team access changes

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that an expired link stops giving access and that changing the team access of the chat does not change its external links.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1 shared with User B (selected people).
- Links: L1 with 1 hour expiration; L2 with Never expires.
- A browser window that is not logged in.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Right after creation, open L1 in the browser that is not logged in | The content opens; the card of L1 is active |
| 2 | Wait until the expiry time of L1 has passed and reload L1 | Access is denied with a clear message; no content |
| 3 | As User A, open Share > Externally | L1 has the badge "Expired" and no expiry date; heading "Active links – 1 · Expired – 1" |
| 4 | As User A, on the Team tab click "Remove access for all" and Save; then switch to Whole team and Save | After each change L2 still opens; the list of links is unchanged |
| 5 | As User B (removed in step 4), open L2 | User B can read it read-only; User B still cannot open C1 in the app |

---

## Expected Final State

Links expire on time and live independently of team access.

---

## Notes

- Step 1 depends on #7653.
