# Test Dashboard

_Generated: 2026-10-22 09:46 UTC_

## Latest Run

**RUN-ELITEA-2026-10-22-311-DEV-CHAT-PASSED**

```mermaid
pie showData
    title "Test Results (0 total)"
    "Passed" : 0
    "Failed" : 0
```

| Metric | Value |
|--------|-------|
| Total | 0 |
| Passed | 0 |
| Failed | 0 |
| Skipped | 0 |
| Reruns | 0 |
| Pass Rate | 0.0% |

## Trend (Last 10 Runs)

```mermaid
xychart-beta
    title "Pass/Fail Trend"
    x-axis [19-298-DEV-CHAT, 19-299-DEV-CHAT, 20-302-DEV-CHAT, 20-303-DEV-CHAT, 21-305-DEV-CHAT, 21-306-DEV-AGENT_HUB, 21-307-DEV-CHAT, 21-308-DEV-CHAT, 22-310-DEV-CHAT, 22-311-DEV-CHAT]
    y-axis "Tests" 0 --> 48
    bar "Passed" [24, 24, 22, 43, 0, 14, 34, 31, 31, 0]
    bar "Failed" [0, 1, 22, 21, 0, 8, 3, 3, 7, 0]
```

### Reruns Trend

```mermaid
xychart-beta
    title "Test Reruns (Flakiness Indicator)"
    x-axis [19-298-DEV-CHAT, 19-299-DEV-CHAT, 20-302-DEV-CHAT, 20-303-DEV-CHAT, 21-305-DEV-CHAT, 21-306-DEV-AGENT_HUB, 21-307-DEV-CHAT, 21-308-DEV-CHAT, 22-310-DEV-CHAT, 22-311-DEV-CHAT]
    y-axis "Reruns" 0 --> 123
    line "Reruns" [2, 4, 60, 120, 0, 30, 8, 0, 6, 0]
```

## Run History

| Run | Total | Passed | Failed | Skipped | Reruns | Rate |
|-----|-------|--------|--------|---------|--------|------|
| ✅ 22-311-DEV-CHAT | 0 | 0 | 0 | 0 | 0 | 0% |
| ❌ 22-310-DEV-CHAT | 40 | 31 | 7 | 2 | 6 | 78% |
| ❌ 21-308-DEV-CHAT | 36 | 31 | 3 | 2 | 0 | 86% |
| ❌ 21-307-DEV-CHAT | 39 | 34 | 3 | 2 | 8 | 87% |
| ❌ 21-306-DEV-AGENT_HUB | 22 | 14 | 8 | 0 | 30 | 64% |
| ✅ 21-305-DEV-CHAT | 0 | 0 | 0 | 0 | 0 | 0% |
| ❌ 20-303-DEV-CHAT | 67 | 43 | 21 | 3 | 120 | 64% |
| ❌ 20-302-DEV-CHAT | 47 | 22 | 22 | 3 | 60 | 47% |
| ❌ 19-299-DEV-CHAT | 27 | 24 | 1 | 2 | 4 | 89% |
| ✅ 19-298-DEV-CHAT | 26 | 24 | 0 | 2 | 2 | 92% |

---
_Source: `reports/automated/junit-RUN-*.json` (20 reports)_

---

## TMS Coverage Analysis

| Metric | Count |
|--------|-------|
| Tests in automation | 274 |
| Tests linked to TMS cases | 272 |
| Tests without TMS case | 2 |
| Orphan TMS refs (test missing) | 0 |
| **TMS Coverage** | **99.3%** |

```mermaid
pie showData
    title "TMS Linkage (274 tests)"
    "Linked to TMS" : 272
    "No TMS case" : 2
```

### Automation Coverage by Suite

| Suite | Automated | Total |
|-------|-----------|-------|
| admin | 3 | 3 |
| agent_hub | 12 | 21 |
| agents | 26 | 61 |
| artifacts | 24 | 80 |
| chat | 40 | 240 |
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
| **All suites** | **247** | **951** |

```mermaid
pie showData
    title "Automated vs Manual (951 cases)"
    "Automated" : 247
    "Manual" : 704
```

```mermaid
pie showData
    title "Automated Cases by Suite (247 of 951)"
    "pipelines" : 89
    "chat" : 40
    "agents" : 26
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
<summary>Show 2 unlinked tests</summary>

- `tests.ui.chat.test_chat_export_download.TestChatExportDownload.test_export_chat_with_messages_without_attachments`
- `tests.ui.chat.test_chat_streaming_response.TestStreamingResponse.test_streaming_response_displayed_progressively`

</details>

---
_Compared `automation/index.json` (274 tests) with `index_automated.json` (272 refs)_
