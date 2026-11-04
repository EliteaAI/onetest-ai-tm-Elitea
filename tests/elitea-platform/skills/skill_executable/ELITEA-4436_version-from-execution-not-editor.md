---
id: ELITEA-4436
title: "Verify version displayed is from run execution, not current editor version"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, version-integrity, metadata]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill has multiple versions OR ability to update version
- User has run history for older version
- Current editor may show newer version

## Test Data

| Field | Value |
|-------|-------|
| Test Scenario | Execute v1.0 → Update to v2.0 → View v1.0 run analytics |
| Metadata Source | runDetails.meta.single_participant.entity_settings.version_id |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create skill with version "v1.0" | Skill created |
| 2 | Execute skill run with v1.0 | Run completes |
| 3 | Update skill to version "v2.0" in editor | Editor now shows v2.0 |
| 4 | Verify editor displays v2.0 | Current version is v2.0 |
| 5 | Navigate to Run History | Run History displays |
| 6 | Locate the v1.0 run in history | Old run visible |
| 7 | Open Analytics for the v1.0 run | Analytics page opens |
| 8 | Observe version displayed in header | Version shown in header |
| 9 | Verify header displays: "Version: v1.0" | Shows EXECUTED version (v1.0) |
| 10 | Verify header does NOT display v2.0 | Does NOT show current editor version |
| 11 | Verify version pulled from runDetails metadata | Source: entity_settings.version_id |
| 12 | Verify historical integrity maintained | Analytics reflects historical execution |

## Expected Final State

Version display:
- Header displays: `Version: v1.0` (executed version)
- Header does NOT display v2.0 (current editor version)
- Version pulled from runDetails.meta.single_participant.entity_settings.version_id
- Historical integrity maintained

## Pass/Fail Criteria

**Pass:**
- Header shows executed version (v1.0)
- Header does NOT show current editor version (v2.0)
- Version source is runDetails metadata
- Historical accuracy maintained

**Fail:**
- Header shows current editor version instead of executed
- Version source incorrect
- Historical accuracy lost
- Confusion between executed and current versions
