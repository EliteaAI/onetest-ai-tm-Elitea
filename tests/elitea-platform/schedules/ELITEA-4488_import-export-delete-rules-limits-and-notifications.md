---
id: ELITEA-4488
title: "Schedules — export and import YAML, delete rules for schedules, versions and entities, project limits, and owner notifications"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:notifications, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011"]
---

# ELITEA-4488: Schedules — export and import YAML, delete rules for schedules, versions and entities, project limits, and owner notifications

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify the remaining epic rules that have no other case: export / import of schedules (admin only; re-import updates in place), what happens on deleting a schedule, a version and an entity, the project limits (minimum 5-minute interval, at most 50 enabled schedules), and the owner's bell notifications (failed, waiting, expired, disabled always; success only with "Get notified").

---

## Preconditions

- **Test data:** import [`qa-sch-agent-basic.agent.md`](../../../test-data/schedules/qa-sch-agent-basic.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- A project admin **ADM** and an editor **ED**; agent **AG** with versions **base** and **v2**; schedules on both versions.
- Settings → General: the "Get notified" switch for schedule success notices.

---

## Steps

### Part A: export / import

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM, Schedules → export one schedule, then several. | YAML `kind: elitea_schedules`, `schema_version`, a `key` per schedule, name, entity name, version name, cron, timezone, prompt, variables, approval rule. No secrets, no ids of other projects. |
| 2 | Import the file into the same project. | Updated in place: same schedule, id, owner, enabled state; no duplicate; no notice for unchanged items. |
| 3 | Delete a schedule, then import the file again. | It is created again **disabled**, owned by the importer. |
| 4 | As ED, export and import. | Refused (403). |

### Part B: delete rules

| # | Action | Expected Result |
|---|--------|-----------------|
| 5 | Delete a schedule. | Gone from the page and the editor card; its past runs stay in Run History. |
| 6 | Delete AG's version **v2**. | Schedules on v2 are **disabled** with a reason, and each owner gets a notice. Schedules on base keep running. |
| 7 | Delete agent AG. | All its schedules are removed. |

### Part C: limits

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | Save a cron more often than every 5 minutes. | "Runs must be at least 5 minutes apart". |
| 9 | With 50 enabled schedules in the project, create or resume one more. | Refused with the project limit message; disabled schedules don't count. (API-assisted setup.) |

### Part D: notifications

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Let a run fail. | The owner gets a "run failed" bell notice with a link to the run. |
| 11 | Let a run wait for approval, then expire. | "needs approval" notice, then 'Schedule "<name>" was not approved in <N> hours and the run stopped'. |
| 12 | Make a schedule get disabled (version deleted, owner lost access). | A "disabled" notice to the owner. |
| 13 | A successful run with "Get notified" off, then on. | Off: no success notice. On: "ran successfully" notice. Failure, approval, expiry and disable notices arrive in both cases. |
| 14 | Click each notice link. | Opens the right run / schedule. |

---

## Expected Final State

The imported schedules match the file; deleted versions and entities left no active schedule behind.

---

## Pass/Fail Criteria

**Pass:**
- All parts behave as above.

**Fail:**
- A re-import duplicates; a deleted version keeps an active schedule; a limit is not enforced; a mandatory notice is missing or a success notice ignores the switch.
