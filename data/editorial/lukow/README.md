# Łuków Editorial Layer

This directory contains human editorial work layered over the selected Łuków graph.

- `record-overrides.json` stores the latest draft for each edited public record.
- `revisions.jsonl` is the append-only edit ledger.
- Every edit is bound to the selected graph checksum.
- Hosted saves are committed through the GitHub API to the configured editorial branch.
- Marking a record ready for review opens or reuses a draft pull request.
- Draft and ready-for-review edits do not change the public projection until that pull request is reviewed and merged.
- Source OCR, evidence ranges, extraction output, and adjudication decisions are immutable.
- Editorial records may add historical context, source interpretation, source-backed
  statements, graph relationships, and links to additional source passages.
- Runtime database and search projections must remain rebuildable from these files.
