# Test Dashboard

_Generated: 2026-10-20 14:48 UTC_

## Latest Run

**RUN-ELITEA-2026-10-20-303-DEV-CHAT-FAILED**

```mermaid
pie showData
    title "Test Results (67 total)"
    "Passed" : 43
    "Failed" : 21
    "Skipped" : 3
```

| Metric | Value |
|--------|-------|
| Total | 67 |
| Passed | 43 |
| Failed | 21 |
| Skipped | 3 |
| Reruns | 120 |
| Pass Rate | 64.2% |

## Trend (Last 10 Runs)

```mermaid
xychart-beta
    title "Pass/Fail Trend"
    x-axis [16-289-DEV-SMOKE, 16-290-DEV-SMOKE, 16-291-DEV-SMOKE, 16-292-DEV-SMOKE, 19-296-DEV-CHAT, 19-297-DEV-CHAT, 19-298-DEV-CHAT, 19-299-DEV-CHAT, 20-302-DEV-CHAT, 20-303-DEV-CHAT]
    y-axis "Tests" 0 --> 48
    bar "Passed" [2, 2, 2, 2, 25, 26, 24, 24, 22, 43]
    bar "Failed" [0, 0, 0, 0, 2, 0, 0, 1, 22, 21]
```

### Reruns Trend

```mermaid
xychart-beta
    title "Test Reruns (Flakiness Indicator)"
    x-axis [16-289-DEV-SMOKE, 16-290-DEV-SMOKE, 16-291-DEV-SMOKE, 16-292-DEV-SMOKE, 19-296-DEV-CHAT, 19-297-DEV-CHAT, 19-298-DEV-CHAT, 19-299-DEV-CHAT, 20-302-DEV-CHAT, 20-303-DEV-CHAT]
    y-axis "Reruns" 0 --> 123
    line "Reruns" [0, 0, 0, 0, 12, 8, 2, 4, 60, 120]
```

## Run History

| Run | Total | Passed | Failed | Skipped | Reruns | Rate |
|-----|-------|--------|--------|---------|--------|------|
| ❌ 20-303-DEV-CHAT | 67 | 43 | 21 | 3 | 120 | 64% |
| ❌ 20-302-DEV-CHAT | 47 | 22 | 22 | 3 | 60 | 47% |
| ❌ 19-299-DEV-CHAT | 27 | 24 | 1 | 2 | 4 | 89% |
| ✅ 19-298-DEV-CHAT | 26 | 24 | 0 | 2 | 2 | 92% |
| ✅ 19-297-DEV-CHAT | 28 | 26 | 0 | 2 | 8 | 93% |
| ❌ 19-296-DEV-CHAT | 29 | 25 | 2 | 2 | 12 | 86% |
| ✅ 16-292-DEV-SMOKE | 2 | 2 | 0 | 0 | 0 | 100% |
| ✅ 16-291-DEV-SMOKE | 2 | 2 | 0 | 0 | 0 | 100% |
| ✅ 16-290-DEV-SMOKE | 2 | 2 | 0 | 0 | 0 | 100% |
| ✅ 16-289-DEV-SMOKE | 2 | 2 | 0 | 0 | 0 | 100% |

---
_Source: `reports/automated/junit-RUN-*.json` (20 reports)_

---

## TMS Coverage Analysis

| Metric | Count |
|--------|-------|
| Tests in automation | 261 |
| Tests linked to TMS cases | 257 |
| Tests without TMS case | 4 |
| Orphan TMS refs (test missing) | 0 |
| **TMS Coverage** | **98.5%** |

```mermaid
pie showData
    title "TMS Linkage (261 tests)"
    "Linked to TMS" : 257
    "No TMS case" : 4
```

### Automation Coverage by Suite

| Suite | Automated | Total |
|-------|-----------|-------|
| admin | 3 | 3 |
| agent_hub | 12 | 21 |
| agents | 26 | 61 |
| artifacts | 24 | 80 |
| chat | 25 | 240 |
| credentials | 1 | 24 |
| evaluation-run-analytics | 0 | 5 |
| help_center | 1 | 12 |
| indexing | 0 | 18 |
| mcp | 3 | 50 |
| onboarding | 0 | 11 |
| per-run-analytics | 0 | 6 |
| pipelines | 89 | 96 |
| settings | 10 | 195 |
| skills | 18 | 66 |
| social-folders | 0 | 13 |
| support-assistant | 14 | 24 |
| toolkit | 0 | 7 |
| toolkits_UI | 6 | 19 |
| **All suites** | **232** | **951** |

```mermaid
pie showData
    title "Automated vs Manual (951 cases)"
    "Automated" : 232
    "Manual" : 719
```

```mermaid
pie showData
    title "Automated Cases by Suite (232 of 951)"
    "pipelines" : 89
    "agents" : 26
    "chat" : 25
    "artifacts" : 24
    "skills" : 18
    "support-assistant" : 14
    "agent_hub" : 12
    "settings" : 10
    "toolkits_UI" : 6
    "admin" : 3
    "mcp" : 3
    "credentials" : 1
    "help_center" : 1
```

### Tests Without TMS Case

_Tests that exist in automation but have no linked TMS case._

<details>
<summary>Show 4 unlinked tests</summary>

- `tests.ui.settings.test_project_context_ai_generation_char_limit.TestProjectContextAIGenerationCharLimit.test_build_with_ai_short_prompt_under_limit`
- `tests.ui.settings.test_project_context_ai_generation_char_limit.TestProjectContextAIGenerationCharLimit.test_build_with_ai_verbose_prompt_exceeds_limit`
- `tests.ui.settings.test_project_context_ai_generation_char_limit.TestProjectContextAIGenerationCharLimit.test_chat_project_context_builder_under_limit`
- `tests.ui.settings.test_project_context_ai_generation_char_limit.TestProjectContextAIGenerationCharLimit.test_edit_with_ai_expand_content_under_limit`

</details>

---
_Compared `automation/index.json` (261 tests) with `index_automated.json` (257 refs)_
