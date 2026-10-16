# Case ID / path change log

Every test case that was **removed, renamed, moved or re-numbered** is recorded here. Use it
to resolve an old id or path found in automation code, reports, dashboards or issues.

- `AFR/` = `tests/automated-full-regression-ui/` · `EP/` = `tests/elitea-platform/`
- Newest entries first. One section per commit. Update this file in the **same commit** as the change.
- Automation repo: `EliteaAI/elitea-testing-public`. Its `@pytest.mark.tms(...)`, `@allure.issue(...)`
  links, AFS file names and `automation_test_id` back-writes follow the id/path recorded here.

## 2026-10-16 — 10 EP cases marked not automated (orphan `tests.ui.*` refs)

Every `automation_test_id` on these cases pointed at a `tests.ui.*` test that does not exist in the automation repo's `main` (`automation/index.json`), and no test there carries their `tms(...)` id. `execution_type` set to `manual`, `automation_test_id` removed; `status: ready` kept. Ids and paths unchanged.

| Case | Path | Removed refs |
|---|---|---|
| ELITEA-0137 | `EP/agents/ELITEA-0137_agent-fixture-data-lifecycle.md` | `tests.ui.agents.test_agent_management.TestAgentIsolation.test_fixture_creates_fresh_agent`, `….test_fixture_cleanup_cycle` |
| ELITEA-0141 | `EP/agents/ELITEA-0141_agent-detail-page-configuration-and-tabs.md` | `tests.ui.agents.test_agent_management.TestAgentConfiguration.test_agent_has_configuration_and_history_tabs` |
| ELITEA-0499 | `EP/chat-interface/ELITEA-0499_chat-message-actions-clear-history.md` | `tests.ui.chat.test_chat_interface.TestConversationUIElements.test_clear_chat_history` |
| ELITEA-0566 | `EP/conversations/ELITEA-0566_conversation-rename-api-direct.md` | `tests.ui.chat.test_conversation_management.TestConversationActions.test_conversation_api_rename` |
| ELITEA-0568 | `EP/conversations/ELITEA-0568_conversation-delete-with-confirmation.md` | `tests.ui.chat.test_conversation_management.TestConversationActions.test_delete_conversation_and_verify_ui` |
| ELITEA-0569 | `EP/conversations/ELITEA-0569_conversation-management-advanced-features.md` | `tests.ui.chat.test_conversation_management.TestConversationList.test_conversation_appears_in_list`, `….TestConversationParticipants.test_add_teammate_to_conversation` |
| ELITEA-0570 | `EP/conversations/ELITEA-0570_conversation-rename-and-delete.md` | `tests.ui.chat.test_conversation_management.TestConversationActions.test_conversation_api_rename`, `….test_delete_conversation_and_verify_ui` |
| ELITEA-0571 | `EP/conversations/ELITEA-0571_conversation-creation-and-list.md` | `tests.ui.chat.test_conversation_management.TestConversationList.test_conversation_appears_in_list` |
| ELITEA-0857 | `EP/pipelines/ELITEA-0857_pipeline-canvas-zoom-and-view-controls.md` | `tests.ui.pipelines.test_pipeline_nodes.TestCanvasInteractions.test_zoom_controls_exist`, `….test_fit_view_adjusts_viewport` |
| ELITEA-0863 | `EP/pipelines/ELITEA-0863_pipeline-node-management.md` | `tests.ui.pipelines.test_pipeline_nodes.TestAddNode.test_add_llm_node`, `….test_add_code_node`, `….TestEditNode.test_edit_node_name`, `….TestConnectNodes.test_connect_node_to_end`, `….TestDeleteNode.test_delete_node_via_menu` |

## 2026-10-16 — remove duplicate custom-theme set ELITEA-4083…4099

Two content-identical copies of the 17 custom-theme cases existed in `AFR/settings/custom-theme/` (all `ready`, none automated). Kept set A ELITEA-4066…4082 (formerly TMS-3543…3559); removed set B ELITEA-4083…4099 (formerly TMS-3579…3595).

| Old id | New id | New path |
|---|---|---|
| ELITEA-4083 (`AFR/settings/custom-theme/ELITEA-4083_project-theme-applies-admin-custom-colors-without-reload.md`) | removed — duplicate of ELITEA-4066 | `AFR/settings/custom-theme/ELITEA-4066_project-theme-applies-admin-custom-colors-without-reload.md` |
| ELITEA-4084 (`AFR/settings/custom-theme/ELITEA-4084_admin-configure-primary-colors-via-color-picker-and-hex.md`) | removed — duplicate of ELITEA-4067 | `AFR/settings/custom-theme/ELITEA-4067_admin-configure-primary-colors-via-color-picker-and-hex.md` |
| ELITEA-4085 (`AFR/settings/custom-theme/ELITEA-4085_custom-logo-upload-replaces-default-in-sidebar.md`) | removed — duplicate of ELITEA-4068 | `AFR/settings/custom-theme/ELITEA-4068_custom-logo-upload-replaces-default-in-sidebar.md` |
| ELITEA-4086 (`AFR/settings/custom-theme/ELITEA-4086_export-json-downloads-custom-theme-configuration.md`) | removed — duplicate of ELITEA-4069 | `AFR/settings/custom-theme/ELITEA-4069_export-json-downloads-custom-theme-configuration.md` |
| ELITEA-4087 (`AFR/settings/custom-theme/ELITEA-4087_import-json-applies-theme-settings-correctly.md`) | removed — duplicate of ELITEA-4070 | `AFR/settings/custom-theme/ELITEA-4070_import-json-applies-theme-settings-correctly.md` |
| ELITEA-4088 (`AFR/settings/custom-theme/ELITEA-4088_admin-theme-changes-reflect-for-all-project-theme-users.md`) | removed — duplicate of ELITEA-4071 | `AFR/settings/custom-theme/ELITEA-4071_admin-theme-changes-reflect-for-all-project-theme-users.md` |
| ELITEA-4089 (`AFR/settings/custom-theme/ELITEA-4089_user-sees-all-four-theme-options-in-preferences.md`) | removed — duplicate of ELITEA-4072 | `AFR/settings/custom-theme/ELITEA-4072_user-sees-all-four-theme-options-in-preferences.md` |
| ELITEA-4090 (`AFR/settings/custom-theme/ELITEA-4090_dark-mode-applies-standard-dark-theme-correctly.md`) | removed — duplicate of ELITEA-4073 | `AFR/settings/custom-theme/ELITEA-4073_dark-mode-applies-standard-dark-theme-correctly.md` |
| ELITEA-4091 (`AFR/settings/custom-theme/ELITEA-4091_light-mode-applies-standard-light-theme-correctly.md`) | removed — duplicate of ELITEA-4074 | `AFR/settings/custom-theme/ELITEA-4074_light-mode-applies-standard-light-theme-correctly.md` |
| ELITEA-4092 (`AFR/settings/custom-theme/ELITEA-4092_system-theme-follows-os-preference.md`) | removed — duplicate of ELITEA-4075 | `AFR/settings/custom-theme/ELITEA-4075_system-theme-follows-os-preference.md` |
| ELITEA-4093 (`AFR/settings/custom-theme/ELITEA-4093_theme-selection-persists-after-page-refresh.md`) | removed — duplicate of ELITEA-4076 | `AFR/settings/custom-theme/ELITEA-4076_theme-selection-persists-after-page-refresh.md` |
| ELITEA-4094 (`AFR/settings/custom-theme/ELITEA-4094_admin-can-access-custom-theme-page-in-admin-portal.md`) | removed — duplicate of ELITEA-4077 | `AFR/settings/custom-theme/ELITEA-4077_admin-can-access-custom-theme-page-in-admin-portal.md` |
| ELITEA-4095 (`AFR/settings/custom-theme/ELITEA-4095_base-mode-dropdown-allows-dark-light-selection.md`) | removed — duplicate of ELITEA-4078 | `AFR/settings/custom-theme/ELITEA-4078_base-mode-dropdown-allows-dark-light-selection.md` |
| ELITEA-4096 (`AFR/settings/custom-theme/ELITEA-4096_background-colors-section-allows-editing-all-values.md`) | removed — duplicate of ELITEA-4079 | `AFR/settings/custom-theme/ELITEA-4079_background-colors-section-allows-editing-all-values.md` |
| ELITEA-4097 (`AFR/settings/custom-theme/ELITEA-4097_border-colors-section-allows-editing-all-values.md`) | removed — duplicate of ELITEA-4080 | `AFR/settings/custom-theme/ELITEA-4080_border-colors-section-allows-editing-all-values.md` |
| ELITEA-4098 (`AFR/settings/custom-theme/ELITEA-4098_delete-theme-resets-to-default-values.md`) | removed — duplicate of ELITEA-4081 | `AFR/settings/custom-theme/ELITEA-4081_delete-theme-resets-to-default-values.md` |
| ELITEA-4099 (`AFR/settings/custom-theme/ELITEA-4099_save-changes-persists-all-custom-theme-modifications.md`) | removed — duplicate of ELITEA-4082 | `AFR/settings/custom-theme/ELITEA-4082_save-changes-persists-all-custom-theme-modifications.md` |

## 2026-10-16 — remove content-identical duplicate cases, renumber the `5889` set, drop stray files

Duplicates verified content-identical (ignoring id/status/automation fields). Rule: keep one copy; prefer AFR over EP; keep the non-`draft` status. None of the affected files carried `automation_test_id` or `execution_type: automated`.

- **5889 ADO process_images set** — two identical copies in `EP/toolkits-credentials/` (ELITEA-2570…2586 and ELITEA-2599…2615, all `ready`). The 2599…2615 copy is removed (frees ELITEA-2599…2614 for the AFR `skills/` cases). The kept copy collided with older, different cases (`EP/toolkits-credentials/aha-toolkit/ELITEA-2570…2582`, `EP/trace-steps-api/ELITEA-2583…2586`), so it is renumbered to free ids ELITEA-4100…4116; the older cases keep their ids.
- **New chat from folder** — `EP/chat-interface/new-chat-from-folder/ELITEA-2753` (`ready`) removed; the identical AFR copy `AFR/chat/ELITEA-2757` kept and set to `status: ready`. `EP/agents/ELITEA-2753_edit-with-ai-…` is a different case and keeps its id.
- **SharePoint read-file-from-sharing-link** — `EP/…/sharepoint/ELITEA-2796…2800` removed (copy of ELITEA-2778…2782, both `draft`, both in EP). `AFR/toolkits_UI/ELITEA-2796…2800_regression-*` are different cases and are now unique.
- **Indexing summaries** — `EP/toolkits-indexes/indexing-summaries/ELITEA-2809…2811` removed (copy of ELITEA-2830…2832, `ready`). `EP/skills/ELITEA-2809`, `EP/skills/ELITEA-2810` and `AFR/chat/ELITEA-2811` are different cases and are now unique.
- **Extension-less files** — `AFR/artifacts/Open MDX File from Artifacts in Preview Mode` (`id: ELITEA-2310`, copy of `EP/artifacts/ELITEA-2310_open-mdx-file-from-artifacts-in-preview-mode.md`) and `AFR/artifacts/Switch from Preview to Raw Mode for MDX files` (`id: ELITEA-2311`, copy of `EP/artifacts/ELITEA-3856_switch-from-preview-to-raw-mode.md`) removed. `AFR/settings/analytics/ELITEA-2311_*` is a different case and is now unique.
- **Stray file** — `EP/indexing/indexing-summaries` (one-line placeholder, not a case) removed.

| Old id | New id | New path |
|---|---|---|
| ELITEA-2570 (`EP/toolkits-credentials/ELITEA-2570_5889-parameter-configuration.md`) | ELITEA-4100 | `EP/toolkits-credentials/ELITEA-4100_5889-parameter-configuration.md` |
| ELITEA-2571 (`EP/toolkits-credentials/ELITEA-2571_5889-image-detection.md`) | ELITEA-4101 | `EP/toolkits-credentials/ELITEA-4101_5889-image-detection.md` |
| ELITEA-2572 (`EP/toolkits-credentials/ELITEA-2572_5889-image-download-validation.md`) | ELITEA-4102 | `EP/toolkits-credentials/ELITEA-4102_5889-image-download-validation.md` |
| ELITEA-2573 (`EP/toolkits-credentials/ELITEA-2573_5889-llm-vision-integration.md`) | ELITEA-4103 | `EP/toolkits-credentials/ELITEA-4103_5889-llm-vision-integration.md` |
| ELITEA-2574 (`EP/toolkits-credentials/ELITEA-2574_5889-image-caching.md`) | ELITEA-4104 | `EP/toolkits-credentials/ELITEA-4104_5889-image-caching.md` |
| ELITEA-2575 (`EP/toolkits-credentials/ELITEA-2575_5889-response-structure.md`) | ELITEA-4105 | `EP/toolkits-credentials/ELITEA-4105_5889-response-structure.md` |
| ELITEA-2576 (`EP/toolkits-credentials/ELITEA-2576_5889-agent-integration.md`) | ELITEA-4106 | `EP/toolkits-credentials/ELITEA-4106_5889-agent-integration.md` |
| ELITEA-2577 (`EP/toolkits-credentials/ELITEA-2577_5889-backward-compatibility.md`) | ELITEA-4107 | `EP/toolkits-credentials/ELITEA-4107_5889-backward-compatibility.md` |
| ELITEA-2578 (`EP/toolkits-credentials/ELITEA-2578_5889-error-handling.md`) | ELITEA-4108 | `EP/toolkits-credentials/ELITEA-4108_5889-error-handling.md` |
| ELITEA-2579 (`EP/toolkits-credentials/ELITEA-2579_5889-image-formats.md`) | ELITEA-4109 | `EP/toolkits-credentials/ELITEA-4109_5889-image-formats.md` |
| ELITEA-2580 (`EP/toolkits-credentials/ELITEA-2580_5889-edge-cases.md`) | ELITEA-4110 | `EP/toolkits-credentials/ELITEA-4110_5889-edge-cases.md` |
| ELITEA-2581 (`EP/toolkits-credentials/ELITEA-2581_5889-configuration-flexibility.md`) | ELITEA-4111 | `EP/toolkits-credentials/ELITEA-4111_5889-configuration-flexibility.md` |
| ELITEA-2582 (`EP/toolkits-credentials/ELITEA-2582_5889-performance-baseline.md`) | ELITEA-4112 | `EP/toolkits-credentials/ELITEA-4112_5889-performance-baseline.md` |
| ELITEA-2583 (`EP/toolkits-credentials/ELITEA-2583_5889-dedicated-tool.md`) | ELITEA-4113 | `EP/toolkits-credentials/ELITEA-4113_5889-dedicated-tool.md` |
| ELITEA-2584 (`EP/toolkits-credentials/ELITEA-2584_5889-monitoring-logging.md`) | ELITEA-4114 | `EP/toolkits-credentials/ELITEA-4114_5889-monitoring-logging.md` |
| ELITEA-2585 (`EP/toolkits-credentials/ELITEA-2585_5889-memory-stability.md`) | ELITEA-4115 | `EP/toolkits-credentials/ELITEA-4115_5889-memory-stability.md` |
| ELITEA-2586 (`EP/toolkits-credentials/ELITEA-2586_5889-error-recovery.md`) | ELITEA-4116 | `EP/toolkits-credentials/ELITEA-4116_5889-error-recovery.md` |
| ELITEA-2599 (`EP/toolkits-credentials/ELITEA-2599_5889-parameter-configuration.md`) | removed — duplicate of ELITEA-4100 | `EP/toolkits-credentials/ELITEA-4100_5889-parameter-configuration.md` |
| ELITEA-2600 (`EP/toolkits-credentials/ELITEA-2600_5889-image-detection.md`) | removed — duplicate of ELITEA-4101 | `EP/toolkits-credentials/ELITEA-4101_5889-image-detection.md` |
| ELITEA-2601 (`EP/toolkits-credentials/ELITEA-2601_5889-image-download-validation.md`) | removed — duplicate of ELITEA-4102 | `EP/toolkits-credentials/ELITEA-4102_5889-image-download-validation.md` |
| ELITEA-2602 (`EP/toolkits-credentials/ELITEA-2602_5889-llm-vision-integration.md`) | removed — duplicate of ELITEA-4103 | `EP/toolkits-credentials/ELITEA-4103_5889-llm-vision-integration.md` |
| ELITEA-2603 (`EP/toolkits-credentials/ELITEA-2603_5889-image-caching.md`) | removed — duplicate of ELITEA-4104 | `EP/toolkits-credentials/ELITEA-4104_5889-image-caching.md` |
| ELITEA-2604 (`EP/toolkits-credentials/ELITEA-2604_5889-response-structure.md`) | removed — duplicate of ELITEA-4105 | `EP/toolkits-credentials/ELITEA-4105_5889-response-structure.md` |
| ELITEA-2605 (`EP/toolkits-credentials/ELITEA-2605_5889-agent-integration.md`) | removed — duplicate of ELITEA-4106 | `EP/toolkits-credentials/ELITEA-4106_5889-agent-integration.md` |
| ELITEA-2606 (`EP/toolkits-credentials/ELITEA-2606_5889-backward-compatibility.md`) | removed — duplicate of ELITEA-4107 | `EP/toolkits-credentials/ELITEA-4107_5889-backward-compatibility.md` |
| ELITEA-2607 (`EP/toolkits-credentials/ELITEA-2607_5889-error-handling.md`) | removed — duplicate of ELITEA-4108 | `EP/toolkits-credentials/ELITEA-4108_5889-error-handling.md` |
| ELITEA-2608 (`EP/toolkits-credentials/ELITEA-2608_5889-image-formats.md`) | removed — duplicate of ELITEA-4109 | `EP/toolkits-credentials/ELITEA-4109_5889-image-formats.md` |
| ELITEA-2609 (`EP/toolkits-credentials/ELITEA-2609_5889-edge-cases.md`) | removed — duplicate of ELITEA-4110 | `EP/toolkits-credentials/ELITEA-4110_5889-edge-cases.md` |
| ELITEA-2610 (`EP/toolkits-credentials/ELITEA-2610_5889-configuration-flexibility.md`) | removed — duplicate of ELITEA-4111 | `EP/toolkits-credentials/ELITEA-4111_5889-configuration-flexibility.md` |
| ELITEA-2611 (`EP/toolkits-credentials/ELITEA-2611_5889-performance-baseline.md`) | removed — duplicate of ELITEA-4112 | `EP/toolkits-credentials/ELITEA-4112_5889-performance-baseline.md` |
| ELITEA-2612 (`EP/toolkits-credentials/ELITEA-2612_5889-dedicated-tool.md`) | removed — duplicate of ELITEA-4113 | `EP/toolkits-credentials/ELITEA-4113_5889-dedicated-tool.md` |
| ELITEA-2613 (`EP/toolkits-credentials/ELITEA-2613_5889-monitoring-logging.md`) | removed — duplicate of ELITEA-4114 | `EP/toolkits-credentials/ELITEA-4114_5889-monitoring-logging.md` |
| ELITEA-2614 (`EP/toolkits-credentials/ELITEA-2614_5889-memory-stability.md`) | removed — duplicate of ELITEA-4115 | `EP/toolkits-credentials/ELITEA-4115_5889-memory-stability.md` |
| ELITEA-2615 (`EP/toolkits-credentials/ELITEA-2615_5889-error-recovery.md`) | removed — duplicate of ELITEA-4116 | `EP/toolkits-credentials/ELITEA-4116_5889-error-recovery.md` |
| ELITEA-2753 (`EP/chat-interface/new-chat-from-folder/ELITEA-2753_chat-new-chat-option-available-in-folder-context-menu.md`) | removed — duplicate of ELITEA-2757 | `AFR/chat/ELITEA-2757_chat-new-chat-option-available-in-folder-context-menu.md` |
| ELITEA-2796 (`EP/toolkits-credentials/sharepoint/ELITEA-2796_read-file-from-sharing-link-oversized-file-no-provider-level-error.md`) | removed — duplicate of ELITEA-2778 | `EP/toolkits-credentials/sharepoint/ELITEA-2778_read-file-from-sharing-link-oversized-file-no-provider-level-error.md` |
| ELITEA-2797 (`EP/toolkits-credentials/sharepoint/ELITEA-2797_read-file-from-sharing-link-bounded-read-start-end-line-and-test-settings-ui.md`) | removed — duplicate of ELITEA-2779 | `EP/toolkits-credentials/sharepoint/ELITEA-2779_read-file-from-sharing-link-bounded-read-start-end-line-and-test-settings-ui.md` |
| ELITEA-2798 (`EP/toolkits-credentials/sharepoint/ELITEA-2798_read-file-from-sharing-link-per-file-type-size-validation-before-download.md`) | removed — duplicate of ELITEA-2780 | `EP/toolkits-credentials/sharepoint/ELITEA-2780_read-file-from-sharing-link-per-file-type-size-validation-before-download.md` |
| ELITEA-2799 (`EP/toolkits-credentials/sharepoint/ELITEA-2799_read-file-from-sharing-link-oversized-excel-workbook-guidance-primary-and-403-fallback.md`) | removed — duplicate of ELITEA-2781 | `EP/toolkits-credentials/sharepoint/ELITEA-2781_read-file-from-sharing-link-oversized-excel-workbook-guidance-primary-and-403-fallback.md` |
| ELITEA-2800 (`EP/toolkits-credentials/sharepoint/ELITEA-2800_read-file-from-sharing-link-invalid-start-end-line-explicit-errors.md`) | removed — duplicate of ELITEA-2782 | `EP/toolkits-credentials/sharepoint/ELITEA-2782_read-file-from-sharing-link-invalid-start-end-line-explicit-errors.md` |
| ELITEA-2809 (`EP/toolkits-indexes/indexing-summaries/ELITEA-2809_unsupported-items-list-formats.md`) | removed — duplicate of ELITEA-2830 | `EP/toolkits-indexes/indexing-summaries/ELITEA-2830_unsupported-items-list-formats.md` |
| ELITEA-2810 (`EP/toolkits-indexes/indexing-summaries/ELITEA-2810_visual-styling-consistency.md`) | removed — duplicate of ELITEA-2831 | `EP/toolkits-indexes/indexing-summaries/ELITEA-2831_visual-styling-consistency.md` |
| ELITEA-2811 (`EP/toolkits-indexes/indexing-summaries/ELITEA-2811_chunk-counts-not-displayed.md`) | removed — duplicate of ELITEA-2832 | `EP/toolkits-indexes/indexing-summaries/ELITEA-2832_chunk-counts-not-displayed.md` |
| ELITEA-2310 (`AFR/artifacts/Open MDX File from Artifacts in Preview Mode`, no extension) | removed — duplicate of ELITEA-2310 | `EP/artifacts/ELITEA-2310_open-mdx-file-from-artifacts-in-preview-mode.md` |
| ELITEA-2311 (`AFR/artifacts/Switch from Preview to Raw Mode for MDX files`, no extension) | removed — duplicate of ELITEA-3856 | `EP/artifacts/ELITEA-3856_switch-from-preview-to-raw-mode.md` |
| — (`EP/indexing/indexing-summaries`, stray placeholder) | removed | — |

## 2026-10-16 — rename `TMS-*` custom-theme cases to the `ELITEA-` format

The 34 cases in `AFR/settings/custom-theme/` used a `TMS-<n>` id/file prefix (PR #150). Renamed to free ids ELITEA-4066 … 4099 (ELITEA-3543 … 3595 are partly taken, so the numbers were not reused). Folder and slug unchanged; `id:` and `# ELITEA-<id>` heading updated. Note: TMS-3579 … 3595 are content-identical copies of TMS-3543 … 3559 (same slugs, only the id differs) — both sets are kept, now as ELITEA-4066 … 4082 and ELITEA-4083 … 4099.

| Old id | New id | New path |
|---|---|---|
| TMS-3543 | ELITEA-4066 | `AFR/settings/custom-theme/ELITEA-4066_project-theme-applies-admin-custom-colors-without-reload.md` |
| TMS-3544 | ELITEA-4067 | `AFR/settings/custom-theme/ELITEA-4067_admin-configure-primary-colors-via-color-picker-and-hex.md` |
| TMS-3545 | ELITEA-4068 | `AFR/settings/custom-theme/ELITEA-4068_custom-logo-upload-replaces-default-in-sidebar.md` |
| TMS-3546 | ELITEA-4069 | `AFR/settings/custom-theme/ELITEA-4069_export-json-downloads-custom-theme-configuration.md` |
| TMS-3547 | ELITEA-4070 | `AFR/settings/custom-theme/ELITEA-4070_import-json-applies-theme-settings-correctly.md` |
| TMS-3548 | ELITEA-4071 | `AFR/settings/custom-theme/ELITEA-4071_admin-theme-changes-reflect-for-all-project-theme-users.md` |
| TMS-3549 | ELITEA-4072 | `AFR/settings/custom-theme/ELITEA-4072_user-sees-all-four-theme-options-in-preferences.md` |
| TMS-3550 | ELITEA-4073 | `AFR/settings/custom-theme/ELITEA-4073_dark-mode-applies-standard-dark-theme-correctly.md` |
| TMS-3551 | ELITEA-4074 | `AFR/settings/custom-theme/ELITEA-4074_light-mode-applies-standard-light-theme-correctly.md` |
| TMS-3552 | ELITEA-4075 | `AFR/settings/custom-theme/ELITEA-4075_system-theme-follows-os-preference.md` |
| TMS-3553 | ELITEA-4076 | `AFR/settings/custom-theme/ELITEA-4076_theme-selection-persists-after-page-refresh.md` |
| TMS-3554 | ELITEA-4077 | `AFR/settings/custom-theme/ELITEA-4077_admin-can-access-custom-theme-page-in-admin-portal.md` |
| TMS-3555 | ELITEA-4078 | `AFR/settings/custom-theme/ELITEA-4078_base-mode-dropdown-allows-dark-light-selection.md` |
| TMS-3556 | ELITEA-4079 | `AFR/settings/custom-theme/ELITEA-4079_background-colors-section-allows-editing-all-values.md` |
| TMS-3557 | ELITEA-4080 | `AFR/settings/custom-theme/ELITEA-4080_border-colors-section-allows-editing-all-values.md` |
| TMS-3558 | ELITEA-4081 | `AFR/settings/custom-theme/ELITEA-4081_delete-theme-resets-to-default-values.md` |
| TMS-3559 | ELITEA-4082 | `AFR/settings/custom-theme/ELITEA-4082_save-changes-persists-all-custom-theme-modifications.md` |
| TMS-3579 | ELITEA-4083 | `AFR/settings/custom-theme/ELITEA-4083_project-theme-applies-admin-custom-colors-without-reload.md` |
| TMS-3580 | ELITEA-4084 | `AFR/settings/custom-theme/ELITEA-4084_admin-configure-primary-colors-via-color-picker-and-hex.md` |
| TMS-3581 | ELITEA-4085 | `AFR/settings/custom-theme/ELITEA-4085_custom-logo-upload-replaces-default-in-sidebar.md` |
| TMS-3582 | ELITEA-4086 | `AFR/settings/custom-theme/ELITEA-4086_export-json-downloads-custom-theme-configuration.md` |
| TMS-3583 | ELITEA-4087 | `AFR/settings/custom-theme/ELITEA-4087_import-json-applies-theme-settings-correctly.md` |
| TMS-3584 | ELITEA-4088 | `AFR/settings/custom-theme/ELITEA-4088_admin-theme-changes-reflect-for-all-project-theme-users.md` |
| TMS-3585 | ELITEA-4089 | `AFR/settings/custom-theme/ELITEA-4089_user-sees-all-four-theme-options-in-preferences.md` |
| TMS-3586 | ELITEA-4090 | `AFR/settings/custom-theme/ELITEA-4090_dark-mode-applies-standard-dark-theme-correctly.md` |
| TMS-3587 | ELITEA-4091 | `AFR/settings/custom-theme/ELITEA-4091_light-mode-applies-standard-light-theme-correctly.md` |
| TMS-3588 | ELITEA-4092 | `AFR/settings/custom-theme/ELITEA-4092_system-theme-follows-os-preference.md` |
| TMS-3589 | ELITEA-4093 | `AFR/settings/custom-theme/ELITEA-4093_theme-selection-persists-after-page-refresh.md` |
| TMS-3590 | ELITEA-4094 | `AFR/settings/custom-theme/ELITEA-4094_admin-can-access-custom-theme-page-in-admin-portal.md` |
| TMS-3591 | ELITEA-4095 | `AFR/settings/custom-theme/ELITEA-4095_base-mode-dropdown-allows-dark-light-selection.md` |
| TMS-3592 | ELITEA-4096 | `AFR/settings/custom-theme/ELITEA-4096_background-colors-section-allows-editing-all-values.md` |
| TMS-3593 | ELITEA-4097 | `AFR/settings/custom-theme/ELITEA-4097_border-colors-section-allows-editing-all-values.md` |
| TMS-3594 | ELITEA-4098 | `AFR/settings/custom-theme/ELITEA-4098_delete-theme-resets-to-default-values.md` |
| TMS-3595 | ELITEA-4099 | `AFR/settings/custom-theme/ELITEA-4099_save-changes-persists-all-custom-theme-modifications.md` |

## 2026-10-16 — help-center ELITEA-3753 marked not automated

`AFR/help_center/ELITEA-3753_help-center-page-loads-successfully-via-sidebar-icon.md` pointed at `tests.ui.help_center.test_help_center_page_loads…`, which does not exist in the automation repo (its PR #2387 went to the frozen `automation/base` branch and never reached `automation/factory` / `main`). Set back to `status: draft`, `execution_type: manual`; `automation_test_id` and `automation_pr` removed. Id and path unchanged.

## 2026-10-16 — ELITEA-3343: keep the AFR version, drop the EP copy, fix the AFR file id

The same case existed twice: `EP/pipelines/entrypoint-trigger-type/ELITEA-3343_oauth-toolkit-restricts-triggers-to-chat-messages-only.md` and `AFR/pipelines/ELITEA-3349_oauth-toolkit-trigger-restriction-chat-only.md`, whose file name said 3349 while its `id:` said 3343. The EP copy is removed; the AFR file keeps its path and its `id:` / heading are now ELITEA-3349 (unused elsewhere).

| Old id | New id | New path | Note |
|---|---|---|---|
| ELITEA-3343 (EP) | — removed | — | kept by the AFR version below |
| ELITEA-3343 (AFR) | ELITEA-3349 | `AFR/pipelines/ELITEA-3349_oauth-toolkit-trigger-restriction-chat-only.md` | id now matches file name |

## 2026-10-16 — renumber PR #169 new case colliding with an existing id

PR #169 (fork published agent carries toolkits) added EP case ELITEA-3761, already taken on main. Renumbered to ELITEA-4065 before merge. Folder and slug unchanged; `id:` and `# ELITEA-<id>` heading updated.

| Old id | New id | New path | Old id kept by |
|---|---|---|---|
| ELITEA-3761 | ELITEA-4065 | `EP/agents-publishing/ELITEA-4065_fork-published-agent-carries-toolkits-mcps-openapi-and-sub-agent-toolkits.md` | `EP/agents/ELITEA-3761_fork-modal-empty-editor-notes.md` |

## 2026-10-16 — renumber PR #166 new cases colliding with existing ids

PR #166 (DIAL API protocol / reasoning / analytics) added 18 EP cases numbered ELITEA-3743 … 3760, all already taken on main. Renumbered to ELITEA-4047 … 4064 before merge. Folder and slug unchanged; `id:` and `# ELITEA-<id>` heading updated.

| Old id | New id | New path | Old id kept by |
|---|---|---|---|
| ELITEA-3743 | ELITEA-4047 | `EP/model-settings/ELITEA-4047_dial-api-protocol-field-visible-only-for-dial-credentials.md` | `AFR/artifacts/ELITEA-3743_verify-all-files-downloadable-when-agent-creates-multiple-files.md` |
| ELITEA-3744 | ELITEA-4048 | `EP/model-settings/ELITEA-4048_dial-api-protocol-persists-on-save-and-reload.md` | `AFR/chat/ELITEA-3744_context-budget-panel-reflects-profile-max-tokens.md` |
| ELITEA-3745 | ELITEA-4049 | `EP/model-settings/ELITEA-4049_dial-model-works-on-recommended-protocol-per-family.md` | `AFR/chat/ELITEA-3745_voice-mini-player-not-visible-by-default-regression.md` |
| ELITEA-3746 | ELITEA-4050 | `EP/model-settings/ELITEA-4050_dial-reasoning-on-and-off-on-correct-protocol.md` | `AFR/admin/ELITEA-3746_blocked-toolkit-live-reload-case-insensitive.md` |
| ELITEA-3747 | ELITEA-4051 | `EP/model-settings/ELITEA-4051_reasoning-validation-applies-on-create-and-update.md` | `AFR/admin/ELITEA-3747_blocked-tool-live-reload-case-insensitive.md` |
| ELITEA-3748 | ELITEA-4052 | `EP/model-settings/ELITEA-4052_non-dial-credential-reasoning-saves-without-protocol-error.md` | `AFR/admin/ELITEA-3748_sensitive-tool-live-reload-case-insensitive.md` |
| ELITEA-3749 | ELITEA-4053 | `EP/model-settings/ELITEA-4053_dial-azure-protocol-reasoning-shows-non-blocking-warning.md` | `AFR/skills/ELITEA-3749_import-skill-base-version.md` |
| ELITEA-3750 | ELITEA-4054 | `EP/model-settings/ELITEA-4054_dial-wrong-protocol-for-model-family-returns-visible-error.md` | `AFR/skills/ELITEA-3750_import-skill-non-base-version.md` |
| ELITEA-3751 | ELITEA-4055 | `EP/model-settings/ELITEA-4055_dial-protocol-change-applies-without-litellm-sync.md` | `AFR/skills/ELITEA-3751_search-skills-by-name.md` |
| ELITEA-3752 | ELITEA-4056 | `EP/model-settings/ELITEA-4056_openai-compatible-toggle-behaviour-for-dial-claude.md` | `AFR/skills/ELITEA-3752_search-skills-by-tag.md` |
| ELITEA-3753 | ELITEA-4057 | `EP/analytics/ELITEA-4057_analytics-run-detail-matches-predict-response.md` | `AFR/help_center/ELITEA-3753_help-center-page-loads-successfully-via-sidebar-icon.md` |
| ELITEA-3754 | ELITEA-4058 | `EP/analytics/ELITEA-4058_run-detail-total-tokens-adds-up-to-agent-totals.md` | `AFR/help_center/ELITEA-3754_help-center-sidebar-interactive-tour-completes-successfully.md` |
| ELITEA-3755 | ELITEA-4059 | `EP/analytics/ELITEA-4059_run-duration-covers-whole-run-including-first-call.md` | `AFR/settings/analytics/ELITEA-3755_analytics-page-loads-with-default-date-range-and-all-six-tab.md` |
| ELITEA-3756 | ELITEA-4060 | `EP/analytics/ELITEA-4060_analytics-aggregates-equal-sum-of-runs.md` | `AFR/artifacts/bucket-permissions/ELITEA-3756_api-no-access-permission-enforcement.md` |
| ELITEA-3757 | ELITEA-4061 | `EP/analytics/ELITEA-4061_costs-by-model-other-row-when-over-display-limit.md` | `AFR/artifacts/bucket-permissions/ELITEA-3757_api-read-only-permission-enforcement.md` |
| ELITEA-3758 | ELITEA-4062 | `EP/analytics/ELITEA-4062_dial-bare-deployment-names-are-priced.md` | `EP/agents/ELITEA-3758_export-nonempty-editor-notes.md` |
| ELITEA-3759 | ELITEA-4063 | `EP/analytics/ELITEA-4063_shared-model-same-name-as-own-model-routes-and-budgets-correctly.md` | `EP/agents/ELITEA-3759_export-empty-editor-notes.md` |
| ELITEA-3760 | ELITEA-4064 | `EP/analytics/ELITEA-4064_per-user-attribution-and-budgets-with-two-users.md` | `EP/agents/ELITEA-3760_fork-modal-nonempty-editor-notes.md` |

## 2026-10-16 — renumber manual/draft id collisions; drop empty automation_test_id

289 cases renumbered (ELITEA-3758 … ELITEA-4046). Rule: if one AFR file is in the group it keeps the id; otherwise the oldest (first-add date) keeps it. Folder and slug unchanged; `id:` and `# ELITEA-<id>` heading updated.

Not touched (same-title copies / id mismatch, awaiting decision): 5889 set 2570–2586 vs 2599–2615, EP 2753 vs AFR 2757, sharepoint 2778–2782 vs 2796–2800, indexing-summaries 2809–2811 vs 2830–2832, AFR 3349 file carrying `id: ELITEA-3343`.

| Old id | New id | New path | Old id kept by |
|---|---|---|---|
| ELITEA-0146 | ELITEA-3758 | `EP/agents/ELITEA-3758_export-nonempty-editor-notes.md` | `EP/agents-publishing/ELITEA-0146_ai-validation-uses-project-level-low-tier-llm-broken-agent-llm-does-no.md` |
| ELITEA-0147 | ELITEA-3759 | `EP/agents/ELITEA-3759_export-empty-editor-notes.md` | `EP/agents-publishing/ELITEA-0147_ai-validation-fallback-agent-level-llm-used-when-project-low-tier-fiel.md` |
| ELITEA-0148 | ELITEA-3760 | `EP/agents/ELITEA-3760_fork-modal-nonempty-editor-notes.md` | `EP/agents-publishing/ELITEA-0148_agent-with-chat-history-save-agent-changes-without-llm-override-error.md` |
| ELITEA-0149 | ELITEA-3761 | `EP/agents/ELITEA-3761_fork-modal-empty-editor-notes.md` | `EP/agents-publishing/ELITEA-0149_validation-report-findings-display-associated-agent-name-main-agent-vs.md` |
| ELITEA-0150 | ELITEA-3762 | `EP/agents/ELITEA-3762_fork-backend-carryover.md` | `EP/agents-publishing/ELITEA-0150_default-ai-validation-prompt-is-used-in-code-as-default-and-matches-im.md` |
| ELITEA-0151 | ELITEA-3763 | `EP/agents/ELITEA-3763_import-exported-agent-with-notes.md` | `EP/agents-publishing/ELITEA-0151_chat-conversation-history-intact-after-agent-version-unpublished.md` |
| ELITEA-0152 | ELITEA-3764 | `EP/agents/ELITEA-3764_export-special-characters.md` | `EP/agents-publishing/ELITEA-0152_chat-messages-from-unpublished-agent-delete-succeeds-regenerate-return.md` |
| ELITEA-0153 | ELITEA-3765 | `EP/agents/ELITEA-3765_export-long-content.md` | `EP/agents-publishing/ELITEA-0153_chat-active-chat-version-unpublished-other-versions-exist-details-edit.md` |
| ELITEA-0154 | ELITEA-3766 | `EP/agents/ELITEA-3766_fork-modal-layout-consistency.md` | `EP/agents-publishing/ELITEA-0154_chat-last-version-unpublished-card-error-details-blocked-chat-fully-no.md` |
| ELITEA-0155 | ELITEA-3767 | `EP/agents/ELITEA-3767_fork-multiple-operations.md` | `EP/agents-publishing/ELITEA-0155_chat-correct-version-specific-icons-shown-when-selecting-a-specific-pu.md` |
| ELITEA-0156 | ELITEA-3768 | `EP/agents/ELITEA-3768_regression-export-metadata.md` | `EP/agents-publishing/ELITEA-0156_agent-icon-displayed-in-agent-studio-and-chat-after-publishing-agent-r.md` |
| ELITEA-0157 | ELITEA-3769 | `EP/agents/ELITEA-3769_regression-fork-modal-sections.md` | `EP/agents-publishing/ELITEA-0157_agent-icon-displayed-in-agent-studio-and-chat-for-agent-with-old-backe.md` |
| ELITEA-0158 | ELITEA-3770 | `EP/agents/ELITEA-3770_regression-editor-notes-editable.md` | `EP/agents-publishing/ELITEA-0158_publishing-blocked-when-a-project-specific-private-model-is-selected-o.md` |
| ELITEA-0890 | ELITEA-3771 | `EP/elitea-chat-bot/ELITEA-3771_stop-button-and-generating-indicator-recover-after-refresh.md` | `EP/pipelines/pipeline-attachments/ELITEA-0890_input-attachments-state-variable-added-removed-when-toggling-attachmen.md` |
| ELITEA-0891 | ELITEA-3772 | `EP/elitea-chat-bot/ELITEA-3772_stop-button-cancels-generation-correctly-once-available-afte.md` | `EP/pipelines/pipeline-attachments/ELITEA-0891_paperclip-icon-becomes-inactive-when-selecting-pipeline-with-allow-att.md` |
| ELITEA-0892 | ELITEA-3773 | `EP/elitea-chat-bot/ELITEA-3773_no-stale-stop-button-or-generating-indicator-shown-when-reop.md` | `EP/pipelines/pipeline-attachments/ELITEA-0892_paperclip-icon-activates-immediately-after-enabling-allow-attachments.md` |
| ELITEA-0893 | ELITEA-3774 | `EP/elitea-chat-bot/ELITEA-3774_normal-uninterrupted-stop-click-during-active-streaming-canc.md` | `EP/pipelines/pipeline-attachments/ELITEA-0893_large-docx-with-many-images-does-not-crash-or-silently-truncate.md` |
| ELITEA-0895 | ELITEA-3775 | `EP/elitea-chat-bot/ELITEA-3775_recovery-targets-the-correct-chat-and-does-not-leak-stop-but.md` | `EP/pipelines/pipeline-attachments/ELITEA-0895_same-filename-attached-twice-auto-renamed-or-conflict-warning-shown.md` |
| ELITEA-1328 | ELITEA-3776 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3776_verify-all-files-downloadable-agent-artifact-toolkit-chat.md` | `tests/pipeline-nodes/ELITEA-1328_bug-4791-code-node-with-import-requests-no-warning-leaked-in-successfu.md` |
| ELITEA-1329 | ELITEA-3777 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3777_verify-all-files-downloadable-pipeline-artifact-toolkit-node.md` | `tests/pipeline-nodes/ELITEA-1329_bug-4791-code-node-runtime-errors-zerodivisionerror-nameerror-syntaxer.md` |
| ELITEA-1330 | ELITEA-3778 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3778_re-validate-single-file-createfile-via-agent-unaffected.md` | `tests/pipeline-nodes/ELITEA-1330_bug-4791-code-node-clean-execution-baseline-http-request-output-and-co.md` |
| ELITEA-1331 | ELITEA-3779 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3779_re-validate-createfile-subfolder-path-single-file-via-chat.md` | `tests/pipeline-nodes/ELITEA-1331_f-string-dropdown-not-triggered-in-state-modifier-and-router-node-fiel.md` |
| ELITEA-1332 | ELITEA-3780 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3780_re-validate-single-file-createfile-via-pipeline-unaffected.md` | `tests/pipeline-nodes/ELITEA-1332_dropdown-renders-correctly-with-large-number-of-state-variables-12.md` |
| ELITEA-1333 | ELITEA-3781 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3781_verify-subfolder-paths-preserved-all-files-multi-file-agent.md` | `tests/pipeline-nodes/ELITEA-1333_all-states-disabled-including-defaults-causes-no-errors-and-dropdown-d.md` |
| ELITEA-1334 | ELITEA-3782 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3782_verify-artifact-file-list-updates-without-refresh-multi-file.md` | `tests/pipeline-nodes/ELITEA-1334_f-string-dropdown-not-triggered-for-fixed-or-variable-field-types-para.md` |
| ELITEA-1335 | ELITEA-3783 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3783_re-validate-file-preview-download-folder-path-files.md` | `tests/pipeline-nodes/ELITEA-1335_variable-references-inserted-via-dropdown-are-correctly-serialized-in.md` |
| ELITEA-1336 | ELITEA-3784 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3784_re-validate-artifact-toolkit-test-settings-createfile-single.md` | `tests/pipeline-nodes/ELITEA-1336_dropdown-reflects-newly-added-state-variable-without-page-reload.md` |
| ELITEA-1337 | ELITEA-3785 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3785_verify-file-count-in-bucket-matches-agent-reported-count.md` | `tests/pipeline-nodes/ELITEA-1337_f-string-dropdown-triggers-filters-by-prefix-and-inserts-variable-corr.md` |
| ELITEA-1338 | ELITEA-3786 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3786_verify-file-timestamps-populated-valid-multi-file-agent-run.md` | `tests/pipeline-nodes/ELITEA-1338_manual-text-inside-not-matching-a-state-variable-is-preserved.md` |
| ELITEA-1339 | ELITEA-3787 | `EP/artifacts/artifacts-toolkit-multi-file/ELITEA-3787_verify-no-ui-errors-console-errors-multi-file-artifact-toolkit.md` | `tests/pipeline-nodes/ELITEA-1339_pending-hitl-notification-appears-when-pipeline-is-paused-and-clears-a.md` |
| ELITEA-1697 | ELITEA-3788 | `EP/admin-portal/guardrails-live-reload/ELITEA-3788_artifacts-tool-not-affected.md` | `EP/toolkits-credentials/ELITEA-1697_selecting-saved-pgvector-credential-works-correctly.md` |
| ELITEA-1698 | ELITEA-3789 | `EP/admin-portal/guardrails-live-reload/ELITEA-3789_guardrails-enforcement-no-regression.md` | `EP/toolkits-credentials/ELITEA-1698_saved-pgvector-credentials-section-heading-displayed-correctly.md` |
| ELITEA-1718 | ELITEA-3790 | `EP/sidebar-menu/personalization/ELITEA-3790_bare-option-appears-in-context-management-modal.md` | `EP/parallel-subagent-hitl/ELITEA-1718_two-parallel-sub-agents-execute-concurrently.md` |
| ELITEA-1719 | ELITEA-3791 | `EP/sidebar-menu/personalization/ELITEA-3791_bare-can-be-selected-and-saved-in-user-settings.md` | `EP/parallel-subagent-hitl/ELITEA-1719_one-sub-agent-failure-does-not-cancel-sibling.md` |
| ELITEA-1720 | ELITEA-3792 | `EP/sidebar-menu/personalization/ELITEA-3792_bare-mode-empty-system-prompt-without-custom-instructions.md` | `EP/parallel-subagent-hitl/ELITEA-1720_both-parallel-sub-agents-hit-sensitive-tools-simultaneously.md` |
| ELITEA-1721 | ELITEA-3793 | `EP/sidebar-menu/personalization/ELITEA-3793_bare-mode-custom-instructions-only.md` | `EP/parallel-subagent-hitl/ELITEA-1721_approve-one-reject-other-routes-independently.md` |
| ELITEA-1722 | ELITEA-3794 | `EP/sidebar-menu/personalization/ELITEA-3794_llm-native-identity-in-bare-mode.md` | `EP/parallel-subagent-hitl/ELITEA-1722_chat-input-disabled-while-hitl-pending.md` |
| ELITEA-1723 | ELITEA-3795 | `EP/sidebar-menu/personalization/ELITEA-3795_context-management-in-bare-mode.md` | `EP/parallel-subagent-hitl/ELITEA-1723_no-stale-hitl-cards-after-completion.md` |
| ELITEA-1735 | ELITEA-3796 | `EP/sensitive-tool-calling/ELITEA-3796_block-with-comment-button-visible-and-expands-comment-input.md` | `AFR/skills/ELITEA-1735_interact-with-skills-from-agent.md` |
| ELITEA-1736 | ELITEA-3797 | `EP/sensitive-tool-calling/ELITEA-3797_block-with-comment-tool-does-not-execute-comment-sent-to-llm.md` | `AFR/skills/ELITEA-1736_interact-with-skills-from-conversation.md` |
| ELITEA-1768 | ELITEA-3798 | `EP/toolkits-credentials/sharepoint/ELITEA-3798_sharepoint-personal-url-delegated-auth-flow-completes-successfully.md` | `EP/pipelines/code-node/ELITEA-1768_code-node-debug-true-artifact-saved-to-code-debug-bucket.md` |
| ELITEA-1769 | ELITEA-3799 | `EP/toolkits-credentials/sharepoint/ELITEA-3799_sharepoint-personal-url-test-connection-validation-succeeds.md` | `EP/pipelines/code-node/ELITEA-1769_code-node-debug-false-or-absent-no-artifact-saved-pipeline-unchanged.md` |
| ELITEA-1770 | ELITEA-3800 | `EP/toolkits-credentials/sharepoint/ELITEA-3800_sharepoint-personal-url-read-txt-file-from-sharing-link.md` | `EP/pipelines/code-node/ELITEA-1770_code-node-multiple-debug-nodes-each-saves-own-artifact.md` |
| ELITEA-2219 | ELITEA-3801 | `EP/agents-publishing/ELITEA-3801_publish-agent-with-skills-happy-path.md` | `EP/mcp-servers/ELITEA-2219_5294-core-logout-functionality.md` |
| ELITEA-2220 | ELITEA-3802 | `EP/agents-publishing/ELITEA-3802_publish-agent-with-sub-agent-skills.md` | `AFR/help_center/ELITEA-2220_help-center-documentation-card-link-redirects-to-external-re.md` |
| ELITEA-2220 | ELITEA-3803 | `EP/mcp-servers/ELITEA-3803_5294-post-logout-mcp-unavailability.md` | `AFR/help_center/ELITEA-2220_help-center-documentation-card-link-redirects-to-external-re.md` |
| ELITEA-2221 | ELITEA-3804 | `EP/agents-publishing/ELITEA-3804_deterministic-validation-short-skill-content.md` | `AFR/help_center/ELITEA-2221_help-center-release-notes-card-link-redirects-to-release-not.md` |
| ELITEA-2221 | ELITEA-3805 | `EP/mcp-servers/ELITEA-3805_5294-login-button-auth-flow.md` | `AFR/help_center/ELITEA-2221_help-center-release-notes-card-link-redirects-to-release-not.md` |
| ELITEA-2222 | ELITEA-3806 | `EP/agents-publishing/ELITEA-3806_deterministic-validation-placeholder-and-secrets.md` | `AFR/help_center/ELITEA-2222_help-center-tutorials-card-link-redirects-to-tutorial-resour.md` |
| ELITEA-2222 | ELITEA-3807 | `EP/mcp-servers/ELITEA-3807_5294-status-indicator-accuracy.md` | `AFR/help_center/ELITEA-2222_help-center-tutorials-card-link-redirects-to-tutorial-resour.md` |
| ELITEA-2223 | ELITEA-3808 | `EP/agents-publishing/ELITEA-3808_ai-validation-harmful-and-jailbreak-content.md` | `AFR/help_center/ELITEA-2223_help-center-video-library-more-redirects-to-full-video-porta.md` |
| ELITEA-2223 | ELITEA-3809 | `EP/mcp-servers/ELITEA-3809_5294-logout-does-not-break-workflow.md` | `AFR/help_center/ELITEA-2223_help-center-video-library-more-redirects-to-full-video-porta.md` |
| ELITEA-2224 | ELITEA-3810 | `EP/agents-publishing/ELITEA-3810_ai-validation-quality-issues-warnings.md` | `AFR/help_center/ELITEA-2224_help-center-tutorials-more-redirects-to-full-tutorials-list.md` |
| ELITEA-2224 | ELITEA-3811 | `EP/mcp-servers/ELITEA-3811_5294-chat-logout-button-visibility.md` | `AFR/help_center/ELITEA-2224_help-center-tutorials-more-redirects-to-full-tutorials-list.md` |
| ELITEA-2225 | ELITEA-3812 | `EP/agents-publishing/ELITEA-3812_publishing-agent-with-warning-level-skill-issues.md` | `AFR/help_center/ELITEA-2225_help-center-version-info-tooltip-displays-component-versions.md` |
| ELITEA-2225 | ELITEA-3813 | `EP/mcp-servers/ELITEA-3813_5294-chat-oauth-custom-headers-auth.md` | `AFR/help_center/ELITEA-2225_help-center-version-info-tooltip-displays-component-versions.md` |
| ELITEA-2226 | ELITEA-3814 | `EP/agents-publishing/ELITEA-3814_validation-token-invalidation-skill-content-modified.md` | `AFR/help_center/ELITEA-2226_help-center-sidebar-interactive-tour-starts-when-clicking-th.md` |
| ELITEA-2226 | ELITEA-3815 | `EP/mcp-servers/ELITEA-3815_5294-chat-state-independence.md` | `AFR/help_center/ELITEA-2226_help-center-sidebar-interactive-tour-starts-when-clicking-th.md` |
| ELITEA-2227 | ELITEA-3816 | `EP/agents-publishing/ELITEA-3816_validation-token-invalidation-add-remove-skill.md` | `EP/mcp-servers/ELITEA-2227_5294-chat-logout-prevents-tools.md` |
| ELITEA-2228 | ELITEA-3817 | `EP/agents-publishing/ELITEA-3817_validation-token-ttl-expiration.md` | `AFR/help_center/ELITEA-2228_help-center-completed-sidebar-interactive-tour-can-be-restar.md` |
| ELITEA-2228 | ELITEA-3818 | `EP/mcp-servers/ELITEA-3818_5294-agent-in-chat-logout-button.md` | `AFR/help_center/ELITEA-2228_help-center-completed-sidebar-interactive-tour-can-be-restar.md` |
| ELITEA-2229 | ELITEA-3819 | `EP/agents-publishing/ELITEA-3819_publishing-flow-without-skills-unaffected.md` | `AFR/help_center/ELITEA-2229_help-center-clicking-skip-during-sidebar-interactive-tour-te.md` |
| ELITEA-2229 | ELITEA-3820 | `EP/mcp-servers/ELITEA-3820_5294-agent-in-chat-oauth-custom.md` | `AFR/help_center/ELITEA-2229_help-center-clicking-skip-during-sidebar-interactive-tour-te.md` |
| ELITEA-2230 | ELITEA-3821 | `EP/agents-publishing/ELITEA-3821_validation-report-without-skills-format-unchanged.md` | `AFR/help_center/ELITEA-2230_help-center-back-button-navigates-to-previous-step-during-in.md` |
| ELITEA-2230 | ELITEA-3822 | `EP/mcp-servers/ELITEA-3822_5294-agent-in-chat-no-cross-impact.md` | `AFR/help_center/ELITEA-2230_help-center-back-button-navigates-to-previous-step-during-in.md` |
| ELITEA-2231 | ELITEA-3823 | `EP/agents-publishing/ELITEA-3823_no-skills-existing-behavior-regression-check.md` | `AFR/onboarding/ELITEA-2231_onboarding-welcome-to-elitea-page-is-displayed-on-first-logi.md` |
| ELITEA-2231 | ELITEA-3824 | `EP/mcp-servers/ELITEA-3824_5294-agent-logout-button-visibility.md` | `AFR/onboarding/ELITEA-2231_onboarding-welcome-to-elitea-page-is-displayed-on-first-logi.md` |
| ELITEA-2232 | ELITEA-3825 | `EP/agents-publishing/ELITEA-3825_unpublish-preserves-skill-attachments.md` | `AFR/onboarding/ELITEA-2232_onboarding-clicking-sure-lets-go-triggers-project-provisioni.md` |
| ELITEA-2232 | ELITEA-3826 | `EP/mcp-servers/ELITEA-3826_5294-agent-oauth-custom-auth.md` | `AFR/onboarding/ELITEA-2232_onboarding-clicking-sure-lets-go-triggers-project-provisioni.md` |
| ELITEA-2233 | ELITEA-3827 | `EP/agents-publishing/ELITEA-3827_re-publish-agent-after-unpublish.md` | `AFR/onboarding/ELITEA-2233_onboarding-elitea-logo-displays-green-dot-indicating-active.md` |
| ELITEA-2233 | ELITEA-3828 | `EP/mcp-servers/ELITEA-3828_5294-agent-logout-clears-state.md` | `AFR/onboarding/ELITEA-2233_onboarding-elitea-logo-displays-green-dot-indicating-active.md` |
| ELITEA-2234 | ELITEA-3829 | `EP/agents-publishing/ELITEA-3829_modify-skills-between-unpublish-and-republish.md` | `AFR/onboarding/ELITEA-2234_onboarding-bell-notification-icon-shows-red-badgedot-on-firs.md` |
| ELITEA-2234 | ELITEA-3830 | `EP/mcp-servers/ELITEA-3830_5294-agent-button-consistency.md` | `AFR/onboarding/ELITEA-2234_onboarding-bell-notification-icon-shows-red-badgedot-on-firs.md` |
| ELITEA-2235 | ELITEA-3831 | `EP/agents-publishing/ELITEA-3831_agent-publish-no-standalone-skill-creation.md` | `AFR/onboarding/ELITEA-2235_onboarding-onboarding-tips-card-is-displayed-on-first-login.md` |
| ELITEA-2235 | ELITEA-3832 | `EP/mcp-servers/ELITEA-3832_5294-toolkit-logout-functionality.md` | `AFR/onboarding/ELITEA-2235_onboarding-onboarding-tips-card-is-displayed-on-first-login.md` |
| ELITEA-2236 | ELITEA-3833 | `EP/agents-publishing/ELITEA-3833_standalone-skill-publish-no-agent-impact.md` | `AFR/onboarding/ELITEA-2236_onboarding-card-can-be-expanded-to-fullscreen-and-collapsed.md` |
| ELITEA-2236 | ELITEA-3834 | `EP/mcp-servers/ELITEA-3834_5294-toolkit-status-display.md` | `AFR/onboarding/ELITEA-2236_onboarding-card-can-be-expanded-to-fullscreen-and-collapsed.md` |
| ELITEA-2237 | ELITEA-3835 | `EP/agents-publishing/ELITEA-3835_modify-standalone-skill-no-agent-snapshot-impact.md` | `AFR/onboarding/ELITEA-2237_onboarding-slides-can-be-navigated-forward-using-the-next-ar.md` |
| ELITEA-2237 | ELITEA-3836 | `EP/mcp-servers/ELITEA-3836_5294-toolkit-login-trigger.md` | `AFR/onboarding/ELITEA-2237_onboarding-slides-can-be-navigated-forward-using-the-next-ar.md` |
| ELITEA-2238 | ELITEA-3837 | `EP/agents-publishing/ELITEA-3837_edge-case-skill-instruction-length-boundaries.md` | `AFR/onboarding/ELITEA-2238_onboarding-left-arrow-is-inactive-on-slide-1-and-right-arrow.md` |
| ELITEA-2238 | ELITEA-3838 | `EP/mcp-servers/ELITEA-3838_5294-toolkit-page-oauth-custom.md` | `AFR/onboarding/ELITEA-2238_onboarding-left-arrow-is-inactive-on-slide-1-and-right-arrow.md` |
| ELITEA-2239 | ELITEA-3839 | `EP/agents-publishing/ELITEA-3839_edge-case-placeholder-detection-in-code-examples.md` | `AFR/onboarding/ELITEA-2239_onboarding-slides-can-be-navigated-forward-and-backward-from.md` |
| ELITEA-2239 | ELITEA-3840 | `EP/toolkits-credentials/ELITEA-3840_5808-update-status-all-9-values.md` | `AFR/onboarding/ELITEA-2239_onboarding-slides-can-be-navigated-forward-and-backward-from.md` |
| ELITEA-2240 | ELITEA-3841 | `EP/agents-publishing/ELITEA-3841_multiple-validation-issues-correct-attribution.md` | `AFR/onboarding/ELITEA-2240_onboarding-private-and-team-projects-appear-in-project-dropd.md` |
| ELITEA-2240 | ELITEA-3842 | `EP/toolkits-credentials/ELITEA-3842_5808-upload-test-case-attachment.md` | `AFR/onboarding/ELITEA-2240_onboarding-private-and-team-projects-appear-in-project-dropd.md` |
| ELITEA-2241 | ELITEA-3843 | `EP/agents-publishing/ELITEA-3843_incremental-fix-validation-updates-correctly.md` | `AFR/onboarding/ELITEA-2241_onboarding-clicking-jump-in-now-closes-onboarding-and-shows.md` |
| ELITEA-2241 | ELITEA-3844 | `EP/toolkits-credentials/ELITEA-3844_5808-upload-test-log-attachment.md` | `AFR/onboarding/ELITEA-2241_onboarding-clicking-jump-in-now-closes-onboarding-and-shows.md` |
| ELITEA-2242 | ELITEA-3845 | `EP/agents-publishing/ELITEA-3845_validation-report-copy-fullscreen-include-all.md` | `AFR/settings/ELITEA-2242_settings-page-loads-and-displays-correct-project-and-persona.md` |
| ELITEA-2242 | ELITEA-3846 | `EP/toolkits-credentials/ELITEA-3846_5808-upload-from-chat-inline.md` | `AFR/settings/ELITEA-2242_settings-page-loads-and-displays-correct-project-and-persona.md` |
| ELITEA-2243 | ELITEA-3847 | `EP/toolkits-credentials/ELITEA-3847_5808-upload-from-artifacts.md` | `AFR/settings/ELITEA-2243_clicking-each-settings-sidebar-item-navigates-to-its-dedicat.md` |
| ELITEA-2244 | ELITEA-3848 | `EP/toolkits-credentials/ELITEA-3848_5808-status-update-with-note.md` | `AFR/settings/ELITEA-2244_navigating-away-from-settings-and-back-restores-the-default.md` |
| ELITEA-2245 | ELITEA-3849 | `EP/toolkits-credentials/ELITEA-3849_5808-error-invalid-testrunid.md` | `AFR/settings/ELITEA-2245_admin-role-has-access-to-all-project-settings-sections.md` |
| ELITEA-2246 | ELITEA-3850 | `EP/toolkits-credentials/ELITEA-3850_5808-error-invalid-status.md` | `AFR/settings/ELITEA-2246_viewer-and-monitor-roles-cannot-access-secrets-section.md` |
| ELITEA-2247 | ELITEA-3851 | `EP/toolkits-credentials/ELITEA-3851_5808-error-invalid-file-source.md` | `AFR/settings/ELITEA-2247_all-authenticated-roles-can-access-personal-settings-section.md` |
| ELITEA-2248 | ELITEA-3852 | `EP/toolkits-credentials/ELITEA-3852_5808-error-invalid-attachmenttype.md` | `AFR/settings/ELITEA-2248_unauthenticated-user-is-redirected-to-login-when-accessing-s.md` |
| ELITEA-2249 | ELITEA-3853 | `EP/toolkits-credentials/ELITEA-3853_5808-attachment-confirmation.md` | `AFR/settings/ELITEA-2249_settings-secrets-page-shows-empty-state-when-no-secrets-exis.md` |
| ELITEA-2250 | ELITEA-3854 | `EP/toolkits-credentials/ELITEA-3854_5808-status-persistence.md` | `AFR/settings/ELITEA-2250_settings-personal-tokens-page-shows-empty-state-when-no-toke.md` |
| ELITEA-2251 | ELITEA-3855 | `EP/toolkits-credentials/ELITEA-3855_5808-attachment-persistence.md` | `AFR/settings/ELITEA-2251_settings-sections-show-loading-state-while-data-is-being-fet.md` |
| ELITEA-2311 | ELITEA-3856 | `EP/artifacts/ELITEA-3856_switch-from-preview-to-raw-mode.md` | `AFR/settings/analytics/ELITEA-2311_overview-tab-displays-all-six-kpi-cards-with-correct-labels.md` |
| ELITEA-2312 | ELITEA-3857 | `EP/artifacts/ELITEA-3857_edit-mdx-in-raw-mode-and-save-changes.md` | `AFR/settings/analytics/ELITEA-2312_users-tab-loads-user-activity-table-with-correct-columns-and.md` |
| ELITEA-2313 | ELITEA-3858 | `EP/artifacts/ELITEA-3858_discard-unsaved-changes.md` | `AFR/settings/analytics/ELITEA-2313_clicking-a-user-row-in-users-tab-opens-the-user-detail-view.md` |
| ELITEA-2314 | ELITEA-3859 | `EP/artifacts/ELITEA-3859_preview-mode-renders-markdown-content-correctly.md` | `AFR/settings/analytics/ELITEA-2314_predefined-date-presets-update-the-fromto-pickers-and-refres.md` |
| ELITEA-2315 | ELITEA-3860 | `EP/artifacts/ELITEA-3860_mdx-with-unsafe-jsx-components-shows-warning.md` | `AFR/settings/analytics/ELITEA-2315_custom-fromto-date-range-filters-data.md` |
| ELITEA-2316 | ELITEA-3861 | `EP/artifacts/ELITEA-3861_open-mdx-file-generated-in-chat.md` | `AFR/settings/analytics/ELITEA-2316_from-date-cannot-be-set-later-than-to-date.md` |
| ELITEA-2317 | ELITEA-3862 | `EP/artifacts/ELITEA-3862_close-canvas-with-unsaved-changes-shows-warning.md` | `AFR/settings/analytics/ELITEA-2317_switching-preset-filters-updates-kpi-cards-charts-and-tables.md` |
| ELITEA-2318 | ELITEA-3863 | `EP/artifacts/ELITEA-3863_unsaved-changes-preserved-when-switching-modes.md` | `AFR/settings/analytics/ELITEA-2318_switching-preset-filters-updates-content-on-agents-tools-and.md` |
| ELITEA-2319 | ELITEA-3864 | `EP/artifacts/ELITEA-3864_preview-refreshes-after-saving-changes.md` | `AFR/settings/analytics/ELITEA-2319_date-filter-is-retained-when-switching-between-tabs.md` |
| ELITEA-2320 | ELITEA-3865 | `EP/artifacts/ELITEA-3865_copy-content-from-three-dot-menu.md` | `AFR/settings/analytics/ELITEA-2320_agents-tab-displays-chat-messages-chart-most-active-agents-b.md` |
| ELITEA-2321 | ELITEA-3866 | `EP/artifacts/ELITEA-3866_download-mdx-file-from-three-dot-menu.md` | `AFR/settings/analytics/ELITEA-2321_clicking-an-agent-row-in-agents-tab-opens-the-agent-detail-v.md` |
| ELITEA-2322 | ELITEA-3867 | `EP/artifacts/ELITEA-3867_mdx-file-listing-in-artifacts-folder-view.md` | `AFR/settings/analytics/ELITEA-2322_tools-tab-displays-most-popular-tools-bar-chart-and-tool-det.md` |
| ELITEA-2323 | ELITEA-3868 | `EP/artifacts/ELITEA-3868_mdx-syntax-highlighting-in-raw-mode.md` | `AFR/settings/analytics/ELITEA-2323_users-tab-search-by-email-filters-the-user-activity-table.md` |
| ELITEA-2324 | ELITEA-3869 | `EP/artifacts/ELITEA-3869_file-type-indicator-shows-mdx-detected.md` | `AFR/settings/analytics/ELITEA-2324_health-tab-displays-requests-vs-errors-chart-and-health-by-e.md` |
| ELITEA-2325 | ELITEA-3870 | `EP/artifacts/ELITEA-3870_medium-sized-mdx-file-performance.md` | `AFR/settings/analytics/ELITEA-2325_guide-tab-displays-explanatory-documentation-for-each-metric.md` |
| ELITEA-2326 | ELITEA-3871 | `EP/artifacts/ELITEA-3871_dark-theme-compatibility-for-mdx-content.md` | `AFR/settings/analytics/ELITEA-2326_hovering-over-daily-activity-chart-on-overview-tab-shows-too.md` |
| ELITEA-2327 | ELITEA-3872 | `EP/artifacts/ELITEA-3872_mdx-with-special-characters-and-unicode.md` | `AFR/settings/analytics/ELITEA-2327_hovering-over-a-bar-in-most-active-agents-chart-shows-agent.md` |
| ELITEA-2328 | ELITEA-3873 | `EP/artifacts/ELITEA-3873_security-script-execution-blocked.md` | `AFR/settings/analytics/ELITEA-2328_hovering-over-most-popular-tools-bar-chart-shows-tool-name-a.md` |
| ELITEA-2329 | ELITEA-3874 | `EP/artifacts/ELITEA-3874_security-import-statements-blocked.md` | `AFR/settings/analytics/ELITEA-2329_hovering-over-user-detail-daily-activity-chart-shows-per-ser.md` |
| ELITEA-2330 | ELITEA-3875 | `EP/artifacts/ELITEA-3875_security-event-handlers-blocked.md` | `AFR/settings/secrets/ELITEA-2330_secrets-page-loads-with-correct-layout-and-components.md` |
| ELITEA-2331 | ELITEA-3876 | `EP/artifacts/ELITEA-3876_empty-mdx-file-opens-without-error.md` | `AFR/settings/secrets/ELITEA-2331_secrets-listing-name-column-is-sortable.md` |
| ELITEA-2478 | ELITEA-3877 | `EP/sidebar-menu/personalization/ELITEA-3877_set-custom-instructions-for-generic-personality.md` | `EP/artifacts/bucket-permissions/ELITEA-2478_add-exception-modal-functionality.md` |
| ELITEA-2479 | ELITEA-3878 | `EP/sidebar-menu/personalization/ELITEA-3878_switch-between-personalities-and-verify-instructions-load.md` | `EP/artifacts/bucket-permissions/ELITEA-2479_edit-single-permission-exception.md` |
| ELITEA-2480 | ELITEA-3879 | `EP/sidebar-menu/personalization/ELITEA-3879_empty-instructions-for-unconfigured-personality.md` | `EP/artifacts/bucket-permissions/ELITEA-2480_bulk-edit-permission-exceptions.md` |
| ELITEA-2481 | ELITEA-3880 | `EP/sidebar-menu/personalization/ELITEA-3880_auto-save-when-switching-personality-without-typing.md` | `EP/artifacts/bucket-permissions/ELITEA-2481_delete-permission-exceptions.md` |
| ELITEA-2482 | ELITEA-3881 | `EP/sidebar-menu/personalization/ELITEA-3881_context-management-off-personality-has-no-effect.md` | `EP/artifacts/bucket-permissions/ELITEA-2482_no-access-permission-enforcement-ui.md` |
| ELITEA-2483 | ELITEA-3882 | `EP/sidebar-menu/personalization/ELITEA-3882_context-management-on-personality-affects-conversation.md` | `EP/artifacts/bucket-permissions/ELITEA-2483_read-permission-enforcement-ui.md` |
| ELITEA-2484 | ELITEA-3883 | `EP/sidebar-menu/personalization/ELITEA-3883_toggle-context-management-from-off-to-on-applies-personality.md` | `EP/artifacts/bucket-permissions/ELITEA-2484_read-write-permission-enforcement-ui.md` |
| ELITEA-2485 | ELITEA-3884 | `EP/sidebar-menu/personalization/ELITEA-3884_settings-personality-change-affects-new-conversations-only.md` | `EP/artifacts/bucket-permissions/ELITEA-2485_api-permission-bypass-no-access.md` |
| ELITEA-2486 | ELITEA-3885 | `EP/sidebar-menu/personalization/ELITEA-3885_auto-save-when-modifying-instruction-text.md` | `EP/artifacts/bucket-permissions/ELITEA-2486_api-permission-bypass-read-only.md` |
| ELITEA-2487 | ELITEA-3886 | `EP/sidebar-menu/personalization/ELITEA-3886_clear-all-instructions-for-a-personality.md` | `EP/artifacts/bucket-permissions/ELITEA-2487_default-permissions-new-user.md` |
| ELITEA-2488 | ELITEA-3887 | `EP/sidebar-menu/personalization/ELITEA-3887_set-instructions-for-all-personality-types.md` | `AFR/artifacts/bucket-permissions/ELITEA-2488_manage-permissions-modal-ui-and-add-no-access-exception.md` |
| ELITEA-2489 | ELITEA-3888 | `EP/sidebar-menu/personalization/ELITEA-3888_long-instruction-text-handling.md` | `AFR/artifacts/bucket-permissions/ELITEA-2489_add-read-only-exception-and-verify-enforcement.md` |
| ELITEA-2490 | ELITEA-3889 | `EP/sidebar-menu/personalization/ELITEA-3889_context-management-instructions-persist-across-sessions.md` | `AFR/artifacts/bucket-permissions/ELITEA-2490_edit-permission-and-bulk-select-all.md` |
| ELITEA-2491 | ELITEA-3890 | `EP/sidebar-menu/personalization/ELITEA-3890_multiple-conversations-with-different-personalities.md` | `AFR/artifacts/bucket-permissions/ELITEA-2491_manage-access-not-visible-in-private-public-projects.md` |
| ELITEA-2492 | ELITEA-3891 | `EP/sidebar-menu/personalization/ELITEA-3891_personality-dropdown-shows-all-types-with-descriptions.md` | `AFR/artifacts/bucket-permissions/ELITEA-2492_empty-state-and-add-exception-flow.md` |
| ELITEA-2493 | ELITEA-3892 | `EP/skills/ELITEA-3892_upload-custom-icon-during-skill-creation-via-create-skill-form.md` | `EP/sidebar-menu/personalization/ELITEA-2493_context-management-inherits-from-settings.md` |
| ELITEA-2493 | ELITEA-3893 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3893_verify-aha-toolkit-appears-in-project-management-category.md` | `EP/sidebar-menu/personalization/ELITEA-2493_context-management-inherits-from-settings.md` |
| ELITEA-2494 | ELITEA-3894 | `EP/skills/ELITEA-3894_upload-and-change-custom-icon-on-edit-skill-form-with-immediate.md` | `EP/sidebar-menu/personalization/ELITEA-2494_same-personality-different-instructions-multiple-conversations.md` |
| ELITEA-2494 | ELITEA-3895 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3895_create-new-aha-toolkit-from-toolkit-button.md` | `EP/sidebar-menu/personalization/ELITEA-2494_same-personality-different-instructions-multiple-conversations.md` |
| ELITEA-2495 | ELITEA-3896 | `EP/skills/ELITEA-3896_custom-icon-displayed-in-skillcard-within-agent-configuration.md` | `EP/sidebar-menu/personalization/ELITEA-2495_copy-paste-instructions-between-personalities.md` |
| ELITEA-2495 | ELITEA-3897 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3897_verify-toolkit-configuration-page-loads-without-errors.md` | `EP/sidebar-menu/personalization/ELITEA-2495_copy-paste-instructions-between-personalities.md` |
| ELITEA-2496 | ELITEA-3898 | `EP/skills/ELITEA-3898_custom-icon-displayed-in-skillmenu-dropdown-skill-picker.md` | `EP/sidebar-menu/personalization/ELITEA-2496_undo-redo-functionality-in-instructions-field.md` |
| ELITEA-2496 | ELITEA-3899 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3899_verify-all-toolkit-form-fields-render-correctly.md` | `EP/sidebar-menu/personalization/ELITEA-2496_undo-redo-functionality-in-instructions-field.md` |
| ELITEA-2497 | ELITEA-3900 | `EP/skills/ELITEA-3900_custom-icon-displayed-in-tilde-mention-autocomplete-list-in-chat.md` | `EP/sidebar-menu/personalization/ELITEA-2497_maximum-character-limit-for-instructions.md` |
| ELITEA-2497 | ELITEA-3901 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3901_create-new-personal-aha-credential-with-all-required-fields.md` | `EP/sidebar-menu/personalization/ELITEA-2497_maximum-character-limit-for-instructions.md` |
| ELITEA-2498 | ELITEA-3902 | `EP/skills/ELITEA-3902_custom-icon-displayed-in-skills-list-page-cardlist-view.md` | `EP/sidebar-menu/personalization/ELITEA-2498_instructions-with-only-whitespace.md` |
| ELITEA-2498 | ELITEA-3903 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3903_verify-new-private-aha-credentials-option-appears-in-dropdown.md` | `EP/sidebar-menu/personalization/ELITEA-2498_instructions-with-only-whitespace.md` |
| ELITEA-2499 | ELITEA-3904 | `EP/skills/ELITEA-3904_viewer-role-cannot-upload-replace-or-delete-skill-icons.md` | `EP/sidebar-menu/personalization/ELITEA-2499_concurrent-editing-from-multiple-browser-tabs.md` |
| ELITEA-2499 | ELITEA-3905 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3905_verify-display-name-field-is-required-and-enforces-validation.md` | `EP/sidebar-menu/personalization/ELITEA-2499_concurrent-editing-from-multiple-browser-tabs.md` |
| ELITEA-2500 | ELITEA-3906 | `EP/skills/ELITEA-3906_skills-without-custom-icon-continue-displaying-default-icon.md` | `EP/sidebar-menu/personalization/ELITEA-2500_browser-back-forward-navigation-behavior.md` |
| ELITEA-2500 | ELITEA-3907 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3907_verify-id-field-is-auto-filled-and-unique.md` | `EP/sidebar-menu/personalization/ELITEA-2500_browser-back-forward-navigation-behavior.md` |
| ELITEA-2501 | ELITEA-3908 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3908_verify-base-url-field-accepts-valid-format.md` | `EP/skills/ELITEA-2501_deleting-an-uploaded-icon-reverts-skills-using-it-to-default.md` |
| ELITEA-2502 | ELITEA-3909 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3909_verify-api-key-field-with-secretpassword-toggle.md` | `EP/skills/ELITEA-2502_file-size-validation-rejects-images-larger-than-500kb.md` |
| ELITEA-2503 | ELITEA-3910 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3910_verify-personal-credential-saves-successfully-with-valid-data.md` | `EP/skills/ELITEA-2503_file-format-validation-accepts-only-allowed-image-types.md` |
| ELITEA-2504 | ELITEA-3911 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3911_verify-personal-credential-appears-in-users-list-only.md` | `EP/skills/ELITEA-2504_uploaded-images-are-resized-rendered-at-maximum-64x64-pixels.md` |
| ELITEA-2505 | ELITEA-3912 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3912_create-new-project-level-aha-credential.md` | `EP/skills/ELITEA-2505_tiff-images-are-handled-with-64x64-dimension-override.md` |
| ELITEA-2511 | ELITEA-3913 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3913_test-connection-with-invalid-api-key.md` | `EP/skills/ELITEA-2511_icon-picker-tooltip-displays-correct-file-size-and-format.md` |
| ELITEA-2512 | ELITEA-3914 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3914_test-connection-with-invalid-base-url-format.md` | `EP/skills/ELITEA-2512_icon-gallery-pagination-works-correctly-for-uploaded-skill-icons.md` |
| ELITEA-2513 | ELITEA-3915 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3915_select-existing-personal-credential-from-dropdown.md` | `EP/skills/ELITEA-2513_selecting-icon-from-existing-gallery-default-section-works.md` |
| ELITEA-2515 | ELITEA-3916 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3916_select-existing-project-credential-from-dropdown.md` | `EP/skills/ELITEA-2515_custom-icon-persists-across-skill-version-operations-save-as.md` |
| ELITEA-2516 | ELITEA-3917 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3917_verify-toolkit-can-use-either-personal-or-project-credential.md` | `EP/skills/ELITEA-2516_admin-role-can-perform-all-icon-operations-upload-replace-delete.md` |
| ELITEA-2517 | ELITEA-3918 | `EP/toolkits-credentials/aha-toolkit/ELITEA-3918_click-refresh-icon-and-verify-credential-list-updates.md` | `EP/skills/ELITEA-2517_editor-role-can-perform-all-icon-operations-upload-replace-delete.md` |
| ELITEA-2590 | ELITEA-3919 | `EP/toolkits-credentials/ELITEA-3919_5844-wiki-non-image-attachment.md` | `EP/trace-steps-api/ELITEA-2590_ui-child-agent-grouping.md` |
| ELITEA-2591 | ELITEA-3920 | `EP/toolkits-credentials/ELITEA-3920_5844-wiki-no-llm-configured.md` | `EP/trace-steps-api/ELITEA-2591_regression-streaming-tool-calls.md` |
| ELITEA-2592 | ELITEA-3921 | `EP/toolkits-credentials/ELITEA-3921_5844-boards-repeated-image-comments.md` | `EP/trace-steps-api/ELITEA-2592_regression-hitl-resume-continue.md` |
| ELITEA-2593 | ELITEA-3922 | `EP/toolkits-credentials/ELITEA-3922_5844-boards-image-comments-attachments.md` | `EP/trace-steps-api/ELITEA-2593_no-duplicate-or-missing-pins.md` |
| ELITEA-2594 | ELITEA-3923 | `EP/toolkits-credentials/ELITEA-3923_5844-boards-prompt-cache-key.md` | `EP/trace-steps-api/ELITEA-2594_trace-steps-invalid-message-group-id.md` |
| ELITEA-2595 | ELITEA-3924 | `EP/toolkits-credentials/ELITEA-3924_5844-boards-process-images-off.md` | `AFR/skills/ELITEA-2595_skill-publishing-wizard-happy-path.md` |
| ELITEA-2596 | ELITEA-3925 | `EP/toolkits-credentials/ELITEA-3925_5844-session-boundary.md` | `AFR/skills/ELITEA-2596_skill-publishing-ai-validation-blockers.md` |
| ELITEA-2597 | ELITEA-3926 | `EP/toolkits-credentials/ELITEA-3926_5844-log-verification.md` | `AFR/skills/ELITEA-2597_skill-publishing-token-invalidation-and-ttl.md` |
| ELITEA-2598 | ELITEA-3927 | `EP/toolkits-credentials/ELITEA-3927_5844-latency-verification.md` | `AFR/skills/ELITEA-2598_skill-publishing-warn-status-scenarios.md` |
| ELITEA-2616 | ELITEA-3928 | `EP/chat-interface/chat_duplicate/ELITEA-3928_duplicate-chat-from-context-menu-creates-independent-chat.md` | `AFR/chat/ELITEA-2616_stop-button-visible-only-during-thinking-phase.md` |
| ELITEA-2616 | ELITEA-3929 | `EP/toolkits-credentials/ELITEA-3929_5999-cloud-auto-happypath.md` | `AFR/chat/ELITEA-2616_stop-button-visible-only-during-thinking-phase.md` |
| ELITEA-2617 | ELITEA-3930 | `EP/chat-interface/chat_duplicate/ELITEA-3930_duplicated-chat-preserves-all-participants-and-configuration.md` | `AFR/chat/ELITEA-2617_stop-during-thinking-restores-exact-input.md` |
| ELITEA-2617 | ELITEA-3931 | `EP/toolkits-credentials/ELITEA-3931_5999-cloud-v3-explicit.md` | `AFR/chat/ELITEA-2617_stop-during-thinking-restores-exact-input.md` |
| ELITEA-2618 | ELITEA-3932 | `EP/chat-interface/chat_duplicate/ELITEA-3932_conversation-independence-between-original-and-duplicate.md` | `AFR/chat/ELITEA-2618_stop-leaves-no-trace-in-chat-history.md` |
| ELITEA-2618 | ELITEA-3933 | `EP/toolkits-credentials/ELITEA-3933_5999-server-auto-v2.md` | `AFR/chat/ELITEA-2618_stop-leaves-no-trace-in-chat-history.md` |
| ELITEA-2619 | ELITEA-3934 | `EP/chat-interface/chat_duplicate/ELITEA-3934_duplicate-chat-persistence-after-page-refresh.md` | `AFR/chat/ELITEA-2619_new-message-sent-normally-immediately-after-stop.md` |
| ELITEA-2619 | ELITEA-3935 | `EP/toolkits-credentials/ELITEA-3935_5999-cloud-forced-v2-mismatch.md` | `AFR/chat/ELITEA-2619_new-message-sent-normally-immediately-after-stop.md` |
| ELITEA-2620 | ELITEA-3936 | `EP/chat-interface/chat_duplicate/ELITEA-3936_duplicate-pinned-chat-unpins-duplicate.md` | `AFR/chat/ELITEA-2620_rapid-double-stop-and-immediate-resend.md` |
| ELITEA-2620 | ELITEA-3937 | `EP/toolkits-credentials/ELITEA-3937_5999-runtime-consistency.md` | `AFR/chat/ELITEA-2620_rapid-double-stop-and-immediate-resend.md` |
| ELITEA-2621 | ELITEA-3938 | `EP/chat-interface/chat_duplicate/ELITEA-3938_duplicate-public-chat-preserves-public-visibility.md` | `AFR/chat/ELITEA-2621_stop-targets-correct-conversation-among-multiple-active.md` |
| ELITEA-2621 | ELITEA-3939 | `EP/toolkits-credentials/ELITEA-3939_5999-agent-execution-path.md` | `AFR/chat/ELITEA-2621_stop-targets-correct-conversation-among-multiple-active.md` |
| ELITEA-2622 | ELITEA-3940 | `EP/chat-interface/chat_duplicate/ELITEA-3940_public-duplicate-visible-to-all-team-members.md` | `AFR/chat/ELITEA-2622_stop-signal-does-not-leak-into-next-generation.md` |
| ELITEA-2622 | ELITEA-3941 | `EP/toolkits-credentials/ELITEA-3941_5999-confluence-cloud-auto.md` | `AFR/chat/ELITEA-2622_stop-signal-does-not-leak-into-next-generation.md` |
| ELITEA-2623 | ELITEA-3942 | `EP/chat-interface/chat_duplicate/ELITEA-3942_duplicate-a-duplicated-public-chat-preserves-visibility.md` | `EP/toolkits-credentials/ELITEA-2623_5999-confluence-server-auto.md` |
| ELITEA-2624 | ELITEA-3943 | `EP/chat-interface/chat_duplicate/ELITEA-3943_duplicate-chat-access-control-security.md` | `EP/toolkits-credentials/ELITEA-2624_5999-confluence-cloud-v2-mismatch.md` |
| ELITEA-2625 | ELITEA-3944 | `EP/chat-interface/chat_duplicate/ELITEA-3944_duplicate-chat-with-ai-participants-only.md` | `EP/toolkits-credentials/ELITEA-2625_5999-confluence-runtime-consistency.md` |
| ELITEA-2626 | ELITEA-3945 | `EP/chat-interface/chat_duplicate/ELITEA-3945_duplicate-chat-preserves-ai-configuration.md` | `EP/toolkits-credentials/ELITEA-2626_5999-confluence-agent-execution.md` |
| ELITEA-2627 | ELITEA-3946 | `EP/chat-interface/chat_duplicate/ELITEA-3946_ai-only-chat-no-unintended-user-participants.md` | `EP/toolkits-credentials/ELITEA-2627_5999-confluence-explicit-v2.md` |
| ELITEA-2754 | ELITEA-3947 | `EP/chat-interface/new-chat-from-folder/ELITEA-3947_chat-new-chat-from-folder-works-in-private-and-team-projects.md` | `EP/agents/ELITEA-2754_edit-with-ai-cta-hidden-for-viewer-role.md` |
| ELITEA-2755 | ELITEA-3948 | `EP/chat-interface/new-chat-from-folder/ELITEA-3948_chat-multiple-consecutive-conversations-created-from-same-folder.md` | `EP/agents/ELITEA-2755_ai-draft-generation-completes-with-loading-state.md` |
| ELITEA-2756 | ELITEA-3949 | `EP/chat-interface/new-chat-from-folder/ELITEA-3949_chat-conversation-operations-after-creating-via-folder-context-menu.md` | `EP/agents/ELITEA-2756_applying-wizard-changes-updates-agent-configuration.md` |
| ELITEA-2757 | ELITEA-3950 | `EP/agents/ELITEA-3950_unchecked-suggestions-excluded-from-applied-result.md` | `AFR/chat/ELITEA-2757_chat-new-chat-option-available-in-folder-context-menu.md` |
| ELITEA-2778 | ELITEA-3951 | `EP/chat-interface/build-skills-project-context/ELITEA-3951_enabling-skills-builder-or-project-context-builder-does-not-regress-ag.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2778_read-file-from-sharing-link-oversized-file-no-provider-level-error.md` |
| ELITEA-2778 | ELITEA-3952 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3952_toolkit-details-two-column-layout-displays-correctly.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2778_read-file-from-sharing-link-oversized-file-no-provider-level-error.md` |
| ELITEA-2779 | ELITEA-3953 | `EP/chat-interface/build-skills-project-context/ELITEA-3953_assistant-does-not-create-a-skill-or-project-context-when-the-correspo.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2779_read-file-from-sharing-link-bounded-read-start-end-line-and-test-settings-ui.md` |
| ELITEA-2779 | ELITEA-3954 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3954_toolkit-config-form-and-raw-json-toggle.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2779_read-file-from-sharing-link-bounded-read-start-end-line-and-test-settings-ui.md` |
| ELITEA-2780 | ELITEA-3955 | `EP/chat-interface/build-skills-project-context/ELITEA-3955_assistant-does-not-hang-when-ask-user-is-disabled-and-required-skill-p.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2780_read-file-from-sharing-link-per-file-type-size-validation-before-download.md` |
| ELITEA-2780 | ELITEA-3956 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3956_toolkit-save-and-discard-changes.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2780_read-file-from-sharing-link-per-file-type-size-validation-before-download.md` |
| ELITEA-2781 | ELITEA-3957 | `EP/chat-interface/build-skills-project-context/ELITEA-3957_headless-api-run-with-auto-skip-enabled-does-not-hang-when-skill-or-pr.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2781_read-file-from-sharing-link-oversized-excel-workbook-guidance-primary-and-403-fallback.md` |
| ELITEA-2781 | ELITEA-3958 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3958_indexes-panel-empty-state-and-create-index.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2781_read-file-from-sharing-link-oversized-excel-workbook-guidance-primary-and-403-fallback.md` |
| ELITEA-2782 | ELITEA-3959 | `EP/chat-interface/build-skills-project-context/ELITEA-3959_sensitive-tool-approval-rejection-hitl-flow-is-unaffected-when-skills.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2782_read-file-from-sharing-link-invalid-start-end-line-explicit-errors.md` |
| ELITEA-2782 | ELITEA-3960 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3960_index-card-display-and-navigation.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2782_read-file-from-sharing-link-invalid-start-end-line-explicit-errors.md` |
| ELITEA-2783 | ELITEA-3961 | `EP/chat-interface/build-skills-project-context/ELITEA-3961_skills-builder-and-project-context-builder-appear-as-independent-toggl.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2783_read-document-regression-check-after-shared-cap-helper-refactor.md` |
| ELITEA-2783 | ELITEA-3962 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3962_index-details-search-button-navigation.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2783_read-document-regression-check-after-shared-cap-helper-refactor.md` |
| ELITEA-2784 | ELITEA-3963 | `EP/chat-interface/build-skills-project-context/ELITEA-3963_skill-creation-from-chat-completes-directly-when-the-request-already-c.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2784_search-page-tool-selection-and-parameters.md` |
| ELITEA-2785 | ELITEA-3964 | `EP/chat-interface/build-skills-project-context/ELITEA-3964_skill-creation-from-chat-with-missing-information-triggers-ask-user-cl.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2785_search-page-execute-search-and-view-results.md` |
| ELITEA-2786 | ELITEA-3965 | `EP/chat-interface/build-skills-project-context/ELITEA-3965_project-context-creation-from-chat-completes-directly-when-the-request.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2786_index-status-indicators-on-cards.md` |
| ELITEA-2787 | ELITEA-3966 | `EP/chat-interface/build-skills-project-context/ELITEA-3966_project-context-update-from-chat-modifies-the-existing-context-instead.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2787_index-details-configuration-and-activity-tabs.md` |
| ELITEA-2788 | ELITEA-3967 | `EP/chat-interface/build-skills-project-context/ELITEA-3967_project-context-creation-update-with-missing-information-triggers-ask.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2788_index-schedule-configuration.md` |
| ELITEA-2789 | ELITEA-3968 | `EP/chat-interface/build-skills-project-context/ELITEA-3968_clarifying-question-control-supports-single-select-multi-select-and-fr.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2789_index-run-history-page.md` |
| ELITEA-2790 | ELITEA-3969 | `EP/chat-interface/build-skills-project-context/ELITEA-3969_multi-question-clarification-flow-shows-correct-progress-indicator-and.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2790_breadcrumb-navigation-throughout-flow.md` |
| ELITEA-2791 | ELITEA-3970 | `EP/chat-interface/build-skills-project-context/ELITEA-3970_single-question-clarification-flow-shows-submit-only-without-progress.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2791_search-tool-switching-clears-parameters.md` |
| ELITEA-2792 | ELITEA-3971 | `EP/chat-interface/build-skills-project-context/ELITEA-3971_optional-clarifying-question-does-not-block-progressing-to-the-next-qu.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2792_tools-section-display-with-tool-count.md` |
| ELITEA-2793 | ELITEA-3972 | `EP/chat-interface/build-skills-project-context/ELITEA-3972_generated-skill-and-project-context-chips-reopen-the-entity-in-canvas.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2793_dark-light-theme-support.md` |
| ELITEA-2794 | ELITEA-3973 | `EP/chat-interface/build-skills-project-context/ELITEA-3973_created-skill-and-project-context-are-not-automatically-added-as-chat.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2794_index-ready-state-with-elitea-chat.md` |
| ELITEA-2795 | ELITEA-3974 | `EP/chat-interface/build-skills-project-context/ELITEA-3974_chat-modules-menu-displays-the-exact-specified-labels-and-tooltip-copy.md` | `EP/toolkits-credentials/toolkits-UI/ELITEA-2795_search-results-copy-and-scroll.md` |
| ELITEA-2796 | ELITEA-3975 | `EP/chat-interface/build-skills-project-context/ELITEA-3975_toggling-skills-builder-or-project-context-builder-mid-conversation-ap.md` | `AFR/toolkits_UI/ELITEA-2796_regression-toolkit-details-layout-and-navigation.md`, `EP/toolkits-credentials/sharepoint/ELITEA-2796_read-file-from-sharing-link-oversized-file-no-provider-level-error.md` |
| ELITEA-2797 | ELITEA-3976 | `EP/chat-interface/build-skills-project-context/ELITEA-3976_clarifying-question-ui-and-resulting-chips-remain-visually-stable-acro.md` | `AFR/toolkits_UI/ELITEA-2797_regression-index-search-functionality.md`, `EP/toolkits-credentials/sharepoint/ELITEA-2797_read-file-from-sharing-link-bounded-read-start-end-line-and-test-settings-ui.md` |
| ELITEA-2798 | ELITEA-3977 | `EP/project-context/ELITEA-3977_retrieve-current-project-context-via-get-project-context.md` | `AFR/toolkits_UI/ELITEA-2798_regression-index-creation-and-status-display.md`, `EP/toolkits-credentials/sharepoint/ELITEA-2798_read-file-from-sharing-link-per-file-type-size-validation-before-download.md` |
| ELITEA-2799 | ELITEA-3978 | `EP/project-context/ELITEA-3978_full-update-of-project-context-sets-both-content-and-enabled-via-put-p.md` | `AFR/toolkits_UI/ELITEA-2799_regression-form-raw-json-toggle-sync.md`, `EP/toolkits-credentials/sharepoint/ELITEA-2799_read-file-from-sharing-link-oversized-excel-workbook-guidance-primary-and-403-fallback.md` |
| ELITEA-2800 | ELITEA-3979 | `EP/project-context/ELITEA-3979_partial-update-omitting-content-must-preserve-existing-content-not-wip.md` | `AFR/toolkits_UI/ELITEA-2800_regression-run-history-and-schedule.md`, `EP/toolkits-credentials/sharepoint/ELITEA-2800_read-file-from-sharing-link-invalid-start-end-line-explicit-errors.md` |
| ELITEA-2801 | ELITEA-3980 | `EP/project-context/ELITEA-3980_updating-project-context-with-an-invalid-project-id-returns-a-clear-ac.md` | `EP/toolkits-credentials/sharepoint/ELITEA-2801_read-document-regression-check-after-shared-cap-helper-refactor.md` |
| ELITEA-2802 | ELITEA-3981 | `EP/indexing/ELITEA-3981_toolkit-run-history-displays-request-parameters-and-detailed-execution-results.md` | `EP/project-context/ELITEA-2802_clean-delete-of-an-existing-project-context-via-delete-project-context.md` |
| ELITEA-2803 | ELITEA-3982 | `EP/mcp-servers/ELITEA-3982_run-history-displays-thinking-steps-and-tools-invoked-for-toolkit-and-mcp.md` | `EP/project-context/ELITEA-2803_repeating-delete-project-context-on-an-already-deleted-context-is-idem.md` |
| ELITEA-2804 | ELITEA-3983 | `EP/toolkits-indexes/indexing-summaries/ELITEA-3983_formatted-summary-replaces-raw-json-index-history.md` | `EP/project-context/ELITEA-2804_deleting-project-context-with-an-invalid-project-id-returns-a-clear-ac.md` |
| ELITEA-2805 | ELITEA-3984 | `EP/toolkits-indexes/indexing-summaries/ELITEA-3984_formatted-summary-in-toolkit-run-history.md` | `EP/project-context/ELITEA-2805_generate-project-context-draft-produces-a-valid-markdown-draft-in-crea.md` |
| ELITEA-2806 | ELITEA-3985 | `EP/toolkits-indexes/indexing-summaries/ELITEA-3985_four-result-categories-display.md` | `EP/project-context/ELITEA-2806_generate-project-context-draft-in-edit-mode-preserves-existing-backgro.md` |
| ELITEA-2807 | ELITEA-3986 | `EP/toolkits-indexes/indexing-summaries/ELITEA-3986_source-appropriate-item-terminology.md` | `EP/project-context/ELITEA-2807_generate-project-context-draft-enforces-the-documented-2500-character.md` |
| ELITEA-2808 | ELITEA-3987 | `EP/toolkits-indexes/indexing-summaries/ELITEA-3987_skipped-items-include-reasons.md` | `EP/project-context/ELITEA-2808_generate-project-context-draft-handles-all-supported-model-name-format.md` |
| ELITEA-2812 | ELITEA-3988 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3988_configuration-section-expanded-by-default.md` | `AFR/chat/ELITEA-2812_followup-suggestions-never-persisted-to-history.md` |
| ELITEA-2813 | ELITEA-3989 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3989_show-more-less-toggle-additional-configuration.md` | `AFR/chat/ELITEA-2813_followup-suggestions-scoped-to-triggering-user-session.md` |
| ELITEA-2814 | ELITEA-3990 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3990_configuration-values-preserved-on-toggle.md` | `AFR/chat/ELITEA-2814_followup-suggestions-global-feature-flag-off.md` |
| ELITEA-2815 | ELITEA-3991 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3991_icon-based-view-mode-controls-with-tooltips.md` | `AFR/chat/ELITEA-2815_followup-suggestions-per-project-disallow-list.md` |
| ELITEA-2816 | ELITEA-3992 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3992_tools-section-collapsed-with-count.md` | `AFR/chat/ELITEA-2816_followup-suggestions-skipped-for-very-short-ai-replies.md` |
| ELITEA-2817 | ELITEA-3993 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3993_tool-enable-disable-updates-header-count.md` | `AFR/chat/ELITEA-2817_followup-suggestions-clear-on-lifecycle-events.md` |
| ELITEA-2818 | ELITEA-3994 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3994_indexes-empty-state-displays-correctly.md` | `AFR/chat/ELITEA-2818_followup-suggestions-failure-timeout-empty-silent-no-op.md` |
| ELITEA-2819 | ELITEA-3995 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3995_reindex-button-disabled-when-index-data-unavailable.md` | `AFR/chat/ELITEA-2819_followup-suggestions-clear-on-source-message-deletion.md` |
| ELITEA-2820 | ELITEA-3996 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3996_section-expand-collapse-state-preserved.md` | `AFR/chat/ELITEA-2820_followup-suggestion-chip-rendering-rules.md` |
| ELITEA-2821 | ELITEA-3997 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3997_dark-light-theme-display-correctly.md` | `AFR/chat/ELITEA-2821_followup-suggestion-chip-click-inserts-editable-text.md` |
| ELITEA-2822 | ELITEA-3998 | `EP/toolkits-credentials/toolkits-UI/ELITEA-3998_section-headers-clickable-expand-collapse.md` | `AFR/chat/ELITEA-2822_followup-suggestion-chip-switch-vs-edit-lock-behavior.md` |
| ELITEA-2823 | ELITEA-3999 | `AFR/toolkits_UI/ELITEA-3999_regression-toolkit-sections-default-states.md` | `AFR/chat/ELITEA-2823_followup-suggestion-chip-keyboard-accessibility-and-visual-states.md` |
| ELITEA-2824 | ELITEA-4000 | `AFR/toolkits_UI/ELITEA-4000_regression-tools-section-count-and-toggle.md` | `AFR/chat/ELITEA-2824_followup-suggestion-chip-list-layout-no-overlap.md` |
| ELITEA-2825 | ELITEA-4001 | `AFR/toolkits_UI/ELITEA-4001_regression-reindex-button-index-data-dependency.md` | `AFR/chat/ELITEA-2825_followup-suggestions-regenerate-response-interaction.md` |
| ELITEA-2830 | ELITEA-4002 | `EP/admin-portal/ELITEA-4002_followup-suggestions-admin-config-min-length-and-generation-timeout.md` | `EP/toolkits-indexes/indexing-summaries/ELITEA-2830_unsupported-items-list-formats.md` |
| ELITEA-2831 | ELITEA-4003 | `EP/admin-portal/ELITEA-4003_disallowed-projects-list-performance-at-15000-project-scale.md` | `EP/toolkits-indexes/indexing-summaries/ELITEA-2831_visual-styling-consistency.md` |
| ELITEA-3194 | ELITEA-4004 | `EP/pipelines/code-node/ELITEA-4004_get-private-project-secret-returns-each-callers-own-value.md` | `EP/social-folders/ELITEA-3194_create-folder-keyboard-behavior-escape-cancel-enter.md` |
| ELITEA-3195 | ELITEA-4005 | `EP/pipelines/code-node/ELITEA-4005_resolved-private-secret-is-genuinely-usable-credential.md` | `EP/social-folders/ELITEA-3195_move-unfiled-entity-into-existing-folder-card-and-table-view.md` |
| ELITEA-3196 | ELITEA-4006 | `EP/pipelines/code-node/ELITEA-4006_unshared-personal-secret-raises-privatesecretnotshared.md` | `EP/social-folders/ELITEA-3196_create-folder-from-move-to-folder-and-auto-assign-entity.md` |
| ELITEA-3197 | ELITEA-4007 | `EP/pipelines/code-node/ELITEA-4007_no-silent-fallback-to-same-named-shared-secret-d5.md` | `EP/social-folders/ELITEA-3197_move-between-folders-and-verify-current-folder-checkmark.md` |
| ELITEA-3198 | ELITEA-4008 | `EP/pipelines/code-node/ELITEA-4008_anti-enumeration-not-shared-and-not-found-indistinguishable.md` | `EP/social-folders/ELITEA-3198_remove-entity-from-folder-card-and-table-view.md` |
| ELITEA-3199 | ELITEA-4009 | `EP/pipelines/code-node/ELITEA-4009_unattended-run-owner-no-personal-project-raises-nopersonalproject.md` | `EP/social-folders/ELITEA-3199_open-populated-folder-filtered-content-header-highlight-indicators-view-persistence.md` |
| ELITEA-3200 | ELITEA-4010 | `EP/pipelines/code-node/ELITEA-4010_unattended-run-resolves-to-owner-identity-regardless-of-last-editor.md` | `EP/social-folders/ELITEA-3200_open-and-close-empty-folder-return-to-complete-list.md` |
| ELITEA-3201 | ELITEA-4011 | `EP/pipelines/code-node/ELITEA-4011_default-param-suppresses-all-three-refusal-reasons.md` | `EP/social-folders/ELITEA-3201_search-across-folders-and-unfiled-entities-with-and-without-open-folder.md` |
| ELITEA-3202 | ELITEA-4012 | `EP/pipelines/code-node/ELITEA-4012_unsecret-shared-secret-behavior-unchanged-regression.md` | `EP/social-folders/ELITEA-3202_rename-folder-preserve-contents-and-open-state.md` |
| ELITEA-3203 | ELITEA-4013 | `EP/pipelines/code-node/ELITEA-4013_special-character-secret-names-both-resolvers.md` | `EP/social-folders/ELITEA-3203_delete-folder-without-deleting-its-entities.md` |
| ELITEA-3204 | ELITEA-4014 | `EP/pipelines/code-node/ELITEA-4014_platform-managed-secret-refused-no-value-leak.md` | `EP/social-folders/ELITEA-3204_folder-isolation-by-entity-type.md` |
| ELITEA-3205 | ELITEA-4015 | `EP/pipelines/code-node/ELITEA-4015_no-secret-value-in-logs-canary-string.md` | `EP/social-folders/ELITEA-3205_folder-isolation-by-project.md` |
| ELITEA-3206 | ELITEA-4016 | `EP/pipelines/code-node/ELITEA-4016_viewer-role-private-secret-access-open-question.md` | `EP/social-folders/ELITEA-3206_folder-scope-boundaries-no-nesting-bulk-assignment-detail-view-assignment.md` |
| ELITEA-3207 | ELITEA-4017 | `EP/secrets/ELITEA-4017_private-secret-toggle-visible-and-persists.md` | `AFR/social-folders/ELITEA-3207_regression-create-folder-autofocus-and-keyboard-behavior.md` |
| ELITEA-3208 | ELITEA-4018 | `EP/secrets/ELITEA-4018_toggle-disabled-while-row-being-edited.md` | `AFR/social-folders/ELITEA-3208_regression-closing-empty-folder-returns-to-complete-list.md` |
| ELITEA-3209 | ELITEA-4019 | `EP/secrets/ELITEA-4019_platform-managed-secret-toggle-disabled-with-tooltip.md` | `AFR/social-folders/ELITEA-3209_regression-deleting-open-folder-returns-to-complete-list.md` |
| ELITEA-3210 | ELITEA-4020 | `EP/secrets/ELITEA-4020_viewer-role-toggle-permission-boundary-open-question.md` | `AFR/social-folders/ELITEA-3210_regression-folder-count-accurate-after-entity-deletion-and-changes.md` |
| ELITEA-3211 | ELITEA-4021 | `EP/secrets/ELITEA-4021_toggle-tooltip-copy-clarity.md` | `AFR/social-folders/ELITEA-3211_regression-selecting-folder-resets-pagination-to-page-1.md` |
| ELITEA-3212 | ELITEA-4022 | `EP/secrets/ELITEA-4022_toggle-save-failure-error-and-rollback.md` | `AFR/social-folders/ELITEA-3212_regression-folder-toast-and-delete-confirmation-copy.md` |
| ELITEA-3213 | ELITEA-4023 | `EP/secrets/ELITEA-4023_toggle-per-row-pending-loading-state.md` | `AFR/social-folders/ELITEA-3213_regression-folder-search-and-highlight-state-persist-across-views.md` |
| ELITEA-3444 | ELITEA-4024 | `EP/conversations/access-control/ELITEA-4024_cancel-make-conversation-public.md` | `AFR/settings/ELITEA-3444_chat-templates-basic-crud-and-default-selection.md` |
| ELITEA-3445 | ELITEA-4025 | `EP/conversations/access-control/ELITEA-4025_successfully-make-conversation-public.md` | `AFR/settings/ELITEA-3445_chat-templates-save-cancel-unsaved-changes.md` |
| ELITEA-3446 | ELITEA-4026 | `EP/conversations/access-control/ELITEA-4026_make-public-hidden-for-public-conversation.md` | `AFR/settings/ELITEA-3446_chat-templates-participants-and-new-chat-behavior.md` |
| ELITEA-3447 | ELITEA-4027 | `EP/conversations/access-control/ELITEA-4027_restrict-access-hidden-for-non-author.md` | `AFR/settings/ELITEA-3447_chat-templates-5-template-limit-and-mid-turn-input.md` |
| ELITEA-1735 | ELITEA-4028 | `EP/sidebar-menu/personalization/ELITEA-4028_verify-personalization-page-loads-with-default-personality-field.md` | `AFR/skills/ELITEA-1735_interact-with-skills-from-agent.md` |
| ELITEA-1736 | ELITEA-4029 | `EP/sidebar-menu/personalization/ELITEA-4029_verify-bare-option-appears-in-default-personality-dropdown.md` | `AFR/skills/ELITEA-1736_interact-with-skills-from-conversation.md` |
| ELITEA-1737 | ELITEA-4030 | `EP/sidebar-menu/personalization/ELITEA-4030_select-bare-personality-and-verify-persistence-after-page-reload.md` | `EP/sensitive-tool-calling/ELITEA-1737_block-with-comment-empty-comment-treated-as-standard-block.md` |
| ELITEA-1738 | ELITEA-4031 | `EP/sidebar-menu/personalization/ELITEA-4031_verify-context-management-modal-opens-and-displays-bare-option.md` | `EP/sensitive-tool-calling/ELITEA-1738_block-with-comment-cancel-returns-to-three-button-state.md` |
| ELITEA-1739 | ELITEA-4032 | `EP/sidebar-menu/personalization/ELITEA-4032_verify-bare-option-in-context-management-user-instructions-dropdown.md` | `EP/sensitive-tool-calling/ELITEA-1739_block-with-comment-long-comment-handled-gracefully.md` |
| ELITEA-1740 | ELITEA-4033 | `EP/sidebar-menu/personalization/ELITEA-4033_create-chat-with-bare-personality-verify-raw-model-identity.md` | `EP/sensitive-tool-calling/ELITEA-1740_block-and-authorize-regression-unaffected-by-block-with-comment.md` |
| ELITEA-1741 | ELITEA-4034 | `EP/sidebar-menu/personalization/ELITEA-4034_switch-from-generic-to-bare-mid-conversation-via-context-management.md` | `EP/sensitive-tool-calling/ELITEA-1741_block-with-comment-recorded-in-hitl-decisions-audit-state.md` |
| ELITEA-1742 | ELITEA-4035 | `EP/sidebar-menu/personalization/ELITEA-4035_test-bare-personality-with-claude-gpt-4-and-gemini-providers.md` | `EP/sensitive-tool-calling/ELITEA-1742_auto-approve-mode-unaffected-block-with-comment-not-shown.md` |
| ELITEA-1743 | ELITEA-4036 | `EP/sidebar-menu/personalization/ELITEA-4036_test-bare-personality-with-custom-instruction-to-respond-in-spanish.md` | `EP/sensitive-tool-calling/ELITEA-1743_block-with-comment-nested-sub-agent-comment-propagates-to-parent.md` |
| ELITEA-2654 | ELITEA-4037 | `tests/alita-sdk/ado/ELITEA-4037_search-code-tool-is-displayed-in-ado-repos-toolkit.md` | `EP/settings/mid-turn-input/ELITEA-2654_send-mid-turn-message-toggle-control.md` |
| ELITEA-2655 | ELITEA-4038 | `tests/alita-sdk/ado/ELITEA-4038_search-code-query-parameter-individual.md` | `EP/settings/mid-turn-input/ELITEA-2655_agent-processes-mid-turn-input.md` |
| ELITEA-2656 | ELITEA-4039 | `tests/alita-sdk/ado/ELITEA-4039_search-code-branch-parameter-individual.md` | `EP/settings/mid-turn-input/ELITEA-2656_mid-turn-message-visible-in-history-after-turn.md` |
| ELITEA-2657 | ELITEA-4040 | `tests/alita-sdk/ado/ELITEA-4040_search-code-path-parameter-individual.md` | `EP/settings/mid-turn-input/ELITEA-2657_conversation-history-persists-on-reload.md` |
| ELITEA-2658 | ELITEA-4041 | `tests/alita-sdk/ado/ELITEA-4041_search-code-top-parameter-individual.md` | `EP/settings/mid-turn-input/ELITEA-2658_stop-button-works-with-mid-turn-input.md` |
| ELITEA-2659 | ELITEA-4042 | `tests/alita-sdk/ado/ELITEA-4042_search-code-skip-parameter-individual.md` | `EP/settings/mid-turn-input/ELITEA-2659_multiple-mid-turn-messages-same-turn.md` |
| ELITEA-2660 | ELITEA-4043 | `tests/alita-sdk/ado/ELITEA-4043_search-code-include-snippets-parameter-individual.md` | `EP/settings/mid-turn-input/ELITEA-2660_mid-turn-input-timing-early.md` |
| ELITEA-2661 | ELITEA-4044 | `tests/alita-sdk/ado/ELITEA-4044_search-code-combined-parameters.md` | `EP/settings/mid-turn-input/ELITEA-2661_mid-turn-input-timing-late-with-ui-feedback.md` |
| ELITEA-2662 | ELITEA-4045 | `tests/alita-sdk/ado/ELITEA-4045_search-code-multiple-searchable-branches.md` | `EP/settings/mid-turn-input/ELITEA-2662_regenerate-after-mid-turn-interaction.md` |
| ELITEA-2663 | ELITEA-4046 | `tests/alita-sdk/ado/ELITEA-4046_search-code-negative-cases.md` | `EP/settings/mid-turn-input/ELITEA-2663_edit-message-after-mid-turn-interaction.md` |

Removed empty `automation_test_id: []` from 34 manual cases:

- `AFR/chat/ELITEA-3603_chat-ampersand-trigger-adds-private-agent-to-participants-filters-and-highlights.md`
- `AFR/chat/ELITEA-3604_chat-trigger-differentiation-hash-shows-all-ampersand-shows-private-plus-shows-users.md`
- `EP/agents/ELITEA-0001_chat-parallel-toolkit-list-collection.md`
- `EP/agents/ELITEA-0136_agent-creation-field-validation.md`
- `EP/agents/ELITEA-0138_agent-edit-operations-name-and-description.md`
- `EP/agents/ELITEA-0140_agent-dashboard-and-search.md`
- `EP/agents/ELITEA-0144_agent-edit-and-delete.md`
- `EP/agents/ELITEA-0145_agent-creation-ui-and-api.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2628_duplicate-chat-with-users-and-ai-participants.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2629_team-project-duplicate-no-participant-crossover.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2630_participant-restrictions-persist-after-refresh.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2631_original-public-chat-has-green-indicator.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2632_duplicated-public-chat-also-has-green-indicator.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2633_duplicate-private-chat-remains-private.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2634_change-duplicate-visibility-original-unaffected.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2635_original-chat-unchanged-after-duplication.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2636_duplicate-naming-convention-with-copy-suffix.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2637_inaccessible-ai-participant-shows-clear-state.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2638_duplicate-action-visible-in-context-menu.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2639_duplicate-appears-at-top-of-chat-list.md`
- `EP/chat-interface/chat_duplicate/ELITEA-2640_participant-panel-rendering-no-regression.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3928_duplicate-chat-from-context-menu-creates-independent-chat.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3930_duplicated-chat-preserves-all-participants-and-configuration.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3932_conversation-independence-between-original-and-duplicate.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3934_duplicate-chat-persistence-after-page-refresh.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3936_duplicate-pinned-chat-unpins-duplicate.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3938_duplicate-public-chat-preserves-public-visibility.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3940_public-duplicate-visible-to-all-team-members.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3942_duplicate-a-duplicated-public-chat-preserves-visibility.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3943_duplicate-chat-access-control-security.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3944_duplicate-chat-with-ai-participants-only.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3945_duplicate-chat-preserves-ai-configuration.md`
- `EP/chat-interface/chat_duplicate/ELITEA-3946_ai-only-chat-no-unintended-user-participants.md`
- `EP/conversations/ELITEA-0567_conversation-fixture-data-lifecycle.md`

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
