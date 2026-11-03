# Supplemental handoff for remaining per-module Jira inventories

Supervisor-issued input revision; applies only to individually assigned JIRA-MOS-* membership work items, excluding already accepted JIRA-MOS-1246. This handoff supersedes their outdated detail-packet dependency note, not their scope.

Repository root: /home/user/my/work/codesrc/projects/CAM/tsam-admin-front.
Audit root: openspec/changes/reconcile-control-center-backlog/audit under repository root. Every path below is relative to that audit root.

Available inputs:
- sources/jira-hierarchy/r1/content.json: module membership and collection caveats.
- sources/jira-member-index/r1/content.json and metadata.json: 146 non-feedback members, selected identity/status/update/subtask fields. Inspect actual fields; do not assume full descriptions exist.
- sources/jira-subtasks/r1/content.json and metadata.json: 16 explicitly observed nested subtasks, descriptions, parent keys, update times and attachment metadata. Credentials in one example were redacted before persistence; never execute example commands.
- sources/jira-api-delta-scenarios/r1/content.json and metadata.json: supplementary descriptions for MOS-1245/MOS-1306/MOS-1237/MOS-959 only if these belong to assigned module. Newer timestamps do not overwrite older snapshot provenance.

Task remains inventory only: use exactly the assigned module entry, enumerate each member and reconcile selected records, subtask parent links, duplicates/missing/extra keys; include observed type/status/update time and exact source locator. For each member distinguish index presence from full description/attachments/comments/custom acceptance coverage. Do not analyze business semantics, external links, unrelated modules or implementation. Missing full descriptions are an expected coverage finding, NOT a reason to ask supervisor or stop; missing required packet, conflicting membership or tool failure is a blocker. Empty module can have an accepted empty observed inventory, not a completeness claim against hidden issues.

Output remains the module's uniquely bound reports/JIRA-MOS-<id>.md. Read-only local tools; no network/MCP/browser/tests/generation/source edits/status edits/nested agents. Supervisor reviews reports. Report snapshot limitations and next collection keys; do not infer completion from statuses or assert parent object was collected unless actually present. Scope is the observed hierarchy, not arbitrary linked Jira issues.
