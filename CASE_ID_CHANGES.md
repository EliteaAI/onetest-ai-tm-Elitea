# Case ID / path change log

Every test case that was **removed, renamed, moved or re-numbered** is recorded here. Use it
to resolve an old id or path found in automation code, reports, dashboards or issues.

- `AFR/` = `tests/automated-full-regression-ui/` · `EP/` = `tests/elitea-platform/`
- Newest entries first. One section per commit. Update this file in the **same commit** as the change.
- Automation repo: `EliteaAI/elitea-testing-public`. Its `@pytest.mark.tms(...)`, `@allure.issue(...)`
  links, AFS file names and `automation_test_id` back-writes follow the id/path recorded here.

## 2026-10-16 — renumber automated cases that collided with unrelated cases

Each of these automated AFR cases had the same `id` as a different, unrelated case
elsewhere in the repo. The automated case got a new unique id: the next free ids after the
max, ELITEA-3743…3757. The slug and folder are unchanged. The colliding cases **keep** their old id.

| Old id | New id | New path | Old id still used by (unchanged) |
|---|---|---|---|
| ELITEA-1694 | ELITEA-3746 | `AFR/admin/ELITEA-3746_blocked-toolkit-live-reload-case-insensitive.md` | `EP/toolkits-credentials/` pgvector |
| ELITEA-1695 | ELITEA-3747 | `AFR/admin/ELITEA-3747_blocked-tool-live-reload-case-insensitive.md` | `EP/toolkits-credentials/` pgvector |
| ELITEA-1696 | ELITEA-3748 | `AFR/admin/ELITEA-3748_sensitive-tool-live-reload-case-insensitive.md` | `EP/toolkits-credentials/` pgvector |
| ELITEA-1327 | ELITEA-3743 | `AFR/artifacts/ELITEA-3743_verify-all-files-downloadable-when-agent-creates-multiple-files.md` | `tests/pipeline-nodes/` Code-node warnings (#4791) |
| ELITEA-2493 | ELITEA-3756 | `AFR/artifacts/bucket-permissions/ELITEA-3756_api-no-access-permission-enforcement.md` | `EP/sidebar-menu/personalization/`, `EP/skills/`, `EP/toolkits-credentials/aha-toolkit/` |
| ELITEA-2494 | ELITEA-3757 | `AFR/artifacts/bucket-permissions/ELITEA-3757_api-read-only-permission-enforcement.md` | `EP/sidebar-menu/personalization/`, `EP/skills/`, `EP/toolkits-credentials/aha-toolkit/` |
| ELITEA-1340 | ELITEA-3744 | `AFR/chat/ELITEA-3744_context-budget-panel-reflects-profile-max-tokens.md` | `tests/pipeline-nodes/` HITL node palette |
| ELITEA-1341 | ELITEA-3745 | `AFR/chat/ELITEA-3745_voice-mini-player-not-visible-by-default-regression.md` | `tests/pipeline-nodes/` HITL three routes |
| ELITEA-2219 | ELITEA-3753 | `AFR/help_center/ELITEA-3753_help-center-page-loads-successfully-via-sidebar-icon.md` | `EP/agents-publishing/`, `EP/mcp-servers/` |
| ELITEA-2227 | ELITEA-3754 | `AFR/help_center/ELITEA-3754_help-center-sidebar-interactive-tour-completes-successfully.md` | `EP/agents-publishing/`, `EP/mcp-servers/` |
| ELITEA-2310 | ELITEA-3755 | `AFR/settings/analytics/ELITEA-3755_analytics-page-loads-with-default-date-range-and-all-six-tab.md` | `EP/artifacts/` MDX preview, `AFR/artifacts/Open MDX File from Artifacts in Preview Mode` |
| ELITEA-1737 | ELITEA-3749 | `AFR/skills/ELITEA-3749_import-skill-base-version.md` | `EP/sensitive-tool-calling/`, `EP/sidebar-menu/personalization/` |
| ELITEA-1738 | ELITEA-3750 | `AFR/skills/ELITEA-3750_import-skill-non-base-version.md` | `EP/sensitive-tool-calling/`, `EP/sidebar-menu/personalization/` |
| ELITEA-1739 | ELITEA-3751 | `AFR/skills/ELITEA-3751_search-skills-by-name.md` | `EP/sensitive-tool-calling/`, `EP/sidebar-menu/personalization/` |
| ELITEA-1740 | ELITEA-3752 | `AFR/skills/ELITEA-3752_search-skills-by-tag.md` | `EP/sensitive-tool-calling/`, `EP/sidebar-menu/personalization/` |

## 2026-10-16 — `481c93c` fix(cases): remove elitea-platform duplicates of AFR cases, fix mcp id mismatches

| Change | Case id | From | To |
|---|---|---|---|
| removed | ELITEA-3712 | `EP/indexing/ELITEA-3712_indexing-completes-successfully-for-medium-sized-repository.md` | — |
| removed | ELITEA-3713 | `EP/indexing/ELITEA-3713_user-receives-notification-when-indexing-completes.md` | — |
| removed | ELITEA-3714 | `EP/indexing/ELITEA-3714_user-receives-notification-when-indexing-is-stopped.md` | — |
| removed | ELITEA-3715 | `EP/indexing/ELITEA-3715_stop-button-stops-indexing-and-shows-stopped-status.md` | — |
| removed | ELITEA-3716 | `EP/indexing/ELITEA-3716_progress-indicator-updates-during-indexing.md` | — |
| removed | ELITEA-3717 | `EP/indexing/ELITEA-3717_error-messages-are-user-friendly.md` | — |
| removed | ELITEA-3718 | `EP/indexing/ELITEA-3718_documents-in-multiple-collections-are-searchable.md` | — |
| removed | ELITEA-2735 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2735_verify-agent-message-displays-toolkit-name-when-authorization-needed.md` | — |
| removed | ELITEA-2736 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2736_verify-multiple-mcps-each-display-correct-toolkit-name-in-agent-message.md` | — |
| removed | ELITEA-2737 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2737_verify-toolkit-name-in-agent-message-from-chat-page.md` | — |
| removed | ELITEA-2738 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2738_verify-nested-agent-displays-toolkit-name-when-authorization-needed.md` | — |
| removed | ELITEA-2739 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2739_verify-nested-agent-with-mcp-from-chat-page.md` | — |
| removed | ELITEA-2740 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2740_verify-pipeline-with-mcp-displays-toolkit-name-in-pipeline-chat.md` | — |
| removed | ELITEA-2741 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2741_verify-pipeline-with-mcp-called-from-chat-page.md` | — |
| removed | ELITEA-2742 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2742_verify-pipeline-with-nested-pipeline-displays-mcp-name-in-pipeline-chat.md` | — |
| removed | ELITEA-2743 | `EP/mcp-servers/toolkit-name-in-auth-prompt/ELITEA-2743_verify-pipeline-with-nested-pipeline-called-from-chat-page.md` | — |
| removed | ELITEA-3472 | `EP/settings/analytics/ELITEA-3472_overview-tab-kpi-cards-display.md` | — |
| removed | ELITEA-3474 | `EP/settings/analytics/ELITEA-3474_overview-top-ai-adopters-leaderboard.md` | — |
| removed | ELITEA-3476 | `EP/settings/analytics/ELITEA-3476_costs-tab-summary-cards.md` | — |
| removed | ELITEA-3480 | `EP/settings/analytics/ELITEA-3480_tokens-tab-summary-cards.md` | — |
| removed | ELITEA-3488 | `EP/settings/analytics/ELITEA-3488_users-tab-activity-table.md` | — |
| removed | ELITEA-3492 | `EP/settings/analytics/ELITEA-3492_health-tab-event-type-table.md` | — |
| removed | ELITEA-3494 | `EP/settings/analytics/ELITEA-3494_date-range-presets.md` | — |
| removed | ELITEA-3497 | `EP/settings/analytics/ELITEA-3497_cross-page-consistency-usage-vs-analytics.md` | — |
| removed | ELITEA-3498 | `EP/settings/analytics/ELITEA-3498_display-name-consistency.md` | — |
| removed | ELITEA-3499 | `EP/settings/analytics/ELITEA-3499_cost-rounding-precision.md` | — |
| id fixed | ELITEA-2750 | frontmatter `id: ELITEA-2741` | `id: ELITEA-2750` (matches filename in `AFR/mcp/toolkit-name-in-auth-prompt/`) |
| id fixed | ELITEA-2751 | frontmatter `id: ELITEA-2742` | `id: ELITEA-2751` (matches filename in `AFR/mcp/toolkit-name-in-auth-prompt/`) |
| id fixed | ELITEA-2752 | frontmatter `id: ELITEA-2743` | `id: ELITEA-2752` (matches filename in `AFR/mcp/toolkit-name-in-auth-prompt/`) |

Removed files were duplicates of the AFR copies, which are kept under the same ids.

## 2026-10-16 — `f3a2a8c` chore(cases): back-write automation ids, rewrite guardrails cases for Jira

| Change | Case id | From | To |
|---|---|---|---|
| moved | ELITEA-1327 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-1327_verify-all-files-downloadable-when-agent-creates-multiple-files.md` | `AFR/artifacts/ELITEA-1327_verify-all-files-downloadable-when-agent-creates-multiple-files.md` |
| removed | ELITEA-1694 | `EP/admin-portal/guardrails-live-reload/ELITEA-1694_blocked-toolkit-live-reload-case-insensitive.md` | — |
| removed | ELITEA-1695 | `EP/admin-portal/guardrails-live-reload/ELITEA-1695_blocked-tool-live-reload-case-insensitive.md` | — |
| removed | ELITEA-1696 | `EP/admin-portal/guardrails-live-reload/ELITEA-1696_sensitive-tool-live-reload-case-insensitive.md` | — |

The removed EP guardrails files duplicated the AFR `admin/` copies (since renumbered to 3746–3748, see above).

## 2026-10-15 — `f11c969` fix: keep api-mapped cases in elitea-platform; harden build-index

| Change | Case id | From | To |
|---|---|---|---|
| moved | ELITEA-0139 | `AFR/agents/ELITEA-0139_agent-export-and-import-yaml-format.md` | `EP/agents/ELITEA-0139_agent-export-and-import-yaml-format.md` |
| moved | ELITEA-0142 | `AFR/agents/ELITEA-0142_agent-export-and-import.md` | `EP/agents/ELITEA-0142_agent-export-and-import.md` |
| moved | ELITEA-0861 | `AFR/pipelines/ELITEA-0861_pipeline-export-and-import.md` | `EP/pipelines/ELITEA-0861_pipeline-export-and-import.md` |
| moved | ELITEA-1050 | `AFR/smoke-suite/ELITEA-1050_api-health-and-connectivity.md` | `EP/smoke-suite/ELITEA-1050_api-health-and-connectivity.md` |
| moved | ELITEA-1052 | `AFR/smoke-suite/ELITEA-1052_platform-availability-basic-navigation.md` | `EP/smoke-suite/ELITEA-1052_platform-availability-basic-navigation.md` |

These moves reverted part of `79e434e`: the cases are API-mapped and stay in EP.

## 2026-10-15 — `79e434e` chore: move automated elitea-platform cases into automated-full-regression-ui suites

| Change | Case id | From | To |
|---|---|---|---|
| moved | ELITEA-0139 | `EP/agents/ELITEA-0139_agent-export-and-import-yaml-format.md` | `AFR/agents/ELITEA-0139_agent-export-and-import-yaml-format.md` |
| moved | ELITEA-0142 | `EP/agents/ELITEA-0142_agent-export-and-import.md` | `AFR/agents/ELITEA-0142_agent-export-and-import.md` |
| moved | ELITEA-1051 | `EP/smoke-suite/ELITEA-1051_chat-basic-functionality.md` | `AFR/chat/ELITEA-1051_chat-basic-functionality.md` |
| moved | ELITEA-1142 | `EP/toolkits-credentials/ELITEA-1142_chat-basic-functionality.md` | `AFR/chat/ELITEA-1142_chat-basic-functionality.md` |
| moved | ELITEA-1340 | `EP/chat-interface/ELITEA-1340_context-budget-panel-reflects-profile-max-tokens.md` | `AFR/chat/ELITEA-1340_context-budget-panel-reflects-profile-max-tokens.md` |
| moved | ELITEA-1341 | `EP/voice/voice-configuration-settings/ELITEA-1341_voice-mini-player-not-visible-by-default-regression.md` | `AFR/chat/ELITEA-1341_voice-mini-player-not-visible-by-default-regression.md` |
| moved | ELITEA-0850 | `EP/pipelines/ELITEA-0850_pipeline-edit-and-delete-operations.md` | `AFR/pipelines/ELITEA-0850_pipeline-edit-and-delete-operations.md` |
| moved | ELITEA-0851 | `EP/pipelines/ELITEA-0851_pipeline-detail-page-configuration-and-tabs.md` | `AFR/pipelines/ELITEA-0851_pipeline-detail-page-configuration-and-tabs.md` |
| moved | ELITEA-0853 | `EP/pipelines/ELITEA-0853_pipeline-node-operations-add-edit-delete-connect.md` | `AFR/pipelines/ELITEA-0853_pipeline-node-operations-add-edit-delete-connect.md` |
| moved | ELITEA-0854 | `EP/pipelines/ELITEA-0854_pipeline-fixture-data-lifecycle.md` | `AFR/pipelines/ELITEA-0854_pipeline-fixture-data-lifecycle.md` |
| moved | ELITEA-0855 | `EP/pipelines/ELITEA-0855_pipeline-dashboard-view-and-search.md` | `AFR/pipelines/ELITEA-0855_pipeline-dashboard-view-and-search.md` |
| moved | ELITEA-0861 | `EP/pipelines/ELITEA-0861_pipeline-export-and-import.md` | `AFR/pipelines/ELITEA-0861_pipeline-export-and-import.md` |
| moved | ELITEA-0864 | `EP/pipelines/ELITEA-0864_pipeline-creation-ui-and-api.md` | `AFR/pipelines/ELITEA-0864_pipeline-creation-ui-and-api.md` |
| moved | ELITEA-1050 | `EP/smoke-suite/ELITEA-1050_api-health-and-connectivity.md` | `AFR/smoke-suite/ELITEA-1050_api-health-and-connectivity.md` |
| moved | ELITEA-1052 | `EP/smoke-suite/ELITEA-1052_platform-availability-basic-navigation.md` | `AFR/smoke-suite/ELITEA-1052_platform-availability-basic-navigation.md` |
| moved | ELITEA-0577 | `EP/elitea-chat-bot/ELITEA-0577_support-assistant-files-can-be-attached-via-click-to-browse-drag-and-d.md` | `AFR/support-assistant/ELITEA-0577_support-assistant-files-can-be-attached-via-click-to-browse-drag-and-d.md` |
| moved | ELITEA-0624 | `EP/elitea-chat-bot/ELITEA-0624_support-assistant-expands-to-full-view-mode-and-collapses-back-to-widg.md` | `AFR/support-assistant/ELITEA-0624_support-assistant-expands-to-full-view-mode-and-collapses-back-to-widg.md` |
| moved | ELITEA-0625 | `EP/elitea-chat-bot/ELITEA-0625_support-assistant-panel-opens-on-launcher-click-and-closes-on-x-button.md` | `AFR/support-assistant/ELITEA-0625_support-assistant-panel-opens-on-launcher-click-and-closes-on-x-button.md` |
| moved | ELITEA-0626 | `EP/elitea-chat-bot/ELITEA-0626_support-assistant-floating-launcher-is-visible-on-every-main-applicati.md` | `AFR/support-assistant/ELITEA-0626_support-assistant-floating-launcher-is-visible-on-every-main-applicati.md` |
| moved | ELITEA-0641 | `EP/elitea-chat-bot/ELITEA-0641_clicking-new-chat-opens-a-clean-session-without-affecting-the-previous.md` | `AFR/support-assistant/ELITEA-0641_clicking-new-chat-opens-a-clean-session-without-affecting-the-previous.md` |
| moved | ELITEA-0643 | `EP/elitea-chat-bot/ELITEA-0643_conversation-is-retained-when-the-support-assistant-panel-is-closed-an.md` | `AFR/support-assistant/ELITEA-0643_conversation-is-retained-when-the-support-assistant-panel-is-closed-an.md` |
| moved | ELITEA-0647 | `EP/elitea-chat-bot/ELITEA-0647_user-sends-a-message-via-the-send-button-and-receives-a-complete-assis.md` | `AFR/support-assistant/ELITEA-0647_user-sends-a-message-via-the-send-button-and-receives-a-complete-assis.md` |

## 2026-10-15 — `e255bd5` chore(tms): move automated cases into suite, fix param refs, drop refs removed in 3fcc147

| Change | Case id | From | To |
|---|---|---|---|
| moved | ELITEA-0059 | `EP/agents/ELITEA-0059_counter-turns-red-when-character-count-reaches-zero-in-full-screen-mod.md` | `AFR/agents/ELITEA-0059_counter-turns-red-when-character-count-reaches-zero-in-full-screen-mod.md` |
| moved | ELITEA-0061 | `EP/agents/ELITEA-0061_counter-turns-red-at-zero-in-collapsed-inline-mode.md` | `AFR/agents/ELITEA-0061_counter-turns-red-at-zero-in-collapsed-inline-mode.md` |
| moved | ELITEA-0062 | `EP/agents/ELITEA-0062_pasting-over-limit-text-text-truncated-to-768-chars-with-visible-feedb.md` | `AFR/agents/ELITEA-0062_pasting-over-limit-text-text-truncated-to-768-chars-with-visible-feedb.md` |
| moved | ELITEA-0063 | `EP/agents/ELITEA-0063_multiple-conversation-starters-have-independent-character-counters.md` | `AFR/agents/ELITEA-0063_multiple-conversation-starters-have-independent-character-counters.md` |
| moved | ELITEA-0064 | `EP/agents/ELITEA-0064_character-counter-is-present-and-updates-in-real-time.md` | `AFR/agents/ELITEA-0064_character-counter-is-present-and-updates-in-real-time.md` |
| moved | ELITEA-0143 | `EP/agents/ELITEA-0143_agent-with-toolkits.md` | `AFR/agents/ELITEA-0143_agent-with-toolkits.md` |
| moved | ELITEA-0498 | `EP/chat-interface/ELITEA-0498_chat-participants-add-via-hash-search.md` | `AFR/chat/ELITEA-0498_chat-participants-add-via-hash-search.md` |
| moved | ELITEA-0500 | `EP/chat-interface/ELITEA-0500_chat-interface-advanced-features.md` | `AFR/chat/ELITEA-0500_chat-interface-advanced-features.md` |
| moved | ELITEA-0502 | `EP/chat-interface/ELITEA-0502_chat-message-actions.md` | `AFR/chat/ELITEA-0502_chat-message-actions.md` |
| moved | ELITEA-0503 | `EP/chat-interface/ELITEA-0503_chat-message-input-methods.md` | `AFR/chat/ELITEA-0503_chat-message-input-methods.md` |
| moved | ELITEA-1049 | `EP/smoke-suite/ELITEA-1049_ui-smoke-test-platform-loads.md` | `AFR/chat/ELITEA-1049_ui-smoke-test-platform-loads.md` |
| moved | ELITEA-1312 | `EP/voice/voice-configuration-settings/ELITEA-1312_voice-settings-dialog-opens-and-displays-all-controls-including-voice.md` | `AFR/chat/ELITEA-1312_voice-settings-dialog-opens-and-displays-all-controls-including-voice.md` |
| moved | ELITEA-1313 | `EP/voice/voice-configuration-settings/ELITEA-1313_voice-settings-dialog-speed-and-volume-sliders-adjust-playback.md` | `AFR/chat/ELITEA-1313_voice-settings-dialog-speed-and-volume-sliders-adjust-playback.md` |
| moved | ELITEA-1314 | `EP/voice/voice-configuration-settings/ELITEA-1314_voice-settings-sync-between-chat-dialog-and-personalization-page.md` | `AFR/chat/ELITEA-1314_voice-settings-sync-between-chat-dialog-and-personalization-page.md` |
| moved | ELITEA-1315 | `EP/voice/voice-configuration-settings/ELITEA-1315_apply-saves-and-cancel-discards-voice-settings-changes.md` | `AFR/chat/ELITEA-1315_apply-saves-and-cancel-discards-voice-settings-changes.md` |
| moved | ELITEA-1316 | `EP/voice/voice-configuration-settings/ELITEA-1316_voice-personalization-page-all-controls-present-including-functional-p.md` | `AFR/chat/ELITEA-1316_voice-personalization-page-all-controls-present-including-functional-p.md` |
| moved | ELITEA-0852 | `EP/pipelines/ELITEA-0852_pipeline-execution-edge-cases.md` | `AFR/pipelines/ELITEA-0852_pipeline-execution-edge-cases.md` |
| moved | ELITEA-0856 | `EP/pipelines/ELITEA-0856_pipeline-execution-message-flow-and-history.md` | `AFR/pipelines/ELITEA-0856_pipeline-execution-message-flow-and-history.md` |
| moved | ELITEA-0858 | `EP/pipelines/ELITEA-0858_pipeline-advanced-node-types.md` | `AFR/pipelines/ELITEA-0858_pipeline-advanced-node-types.md` |
| moved | ELITEA-0859 | `EP/pipelines/ELITEA-0859_pipeline-three-dot-menu-and-actions.md` | `AFR/pipelines/ELITEA-0859_pipeline-three-dot-menu-and-actions.md` |
| moved | ELITEA-0860 | `EP/pipelines/ELITEA-0860_pipeline-yaml-view-and-round-trip.md` | `AFR/pipelines/ELITEA-0860_pipeline-yaml-view-and-round-trip.md` |
| moved | ELITEA-0862 | `EP/pipelines/ELITEA-0862_pipeline-execution.md` | `AFR/pipelines/ELITEA-0862_pipeline-execution.md` |
| moved | ELITEA-1180 | `EP/toolkits-credentials/credential-actions-and-status-indicators/ELITEA-1180_open-in-new-tab-icon-is-present-for-all-credentials-regardless-of-stat.md` | `AFR/toolkits_UI/ELITEA-1180_open-in-new-tab-icon-is-present-for-all-credentials-regardless-of-stat.md` |
| moved | ELITEA-1181 | `EP/toolkits-credentials/credential-actions-and-status-indicators/ELITEA-1181_verify-reload-applies-fixes-of-credentials-immediately.md` | `AFR/toolkits_UI/ELITEA-1181_verify-reload-applies-fixes-of-credentials-immediately.md` |
| moved | ELITEA-1183 | `EP/toolkits-credentials/credential-actions-and-status-indicators/ELITEA-1183_toolkit-displays-authentication-warning-and-disables-save-for-invalid.md` | `AFR/toolkits_UI/ELITEA-1183_toolkit-displays-authentication-warning-and-disables-save-for-invalid.md` |
