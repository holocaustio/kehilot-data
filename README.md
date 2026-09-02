# kehilot-data

Canonical data for the [Kehilot](https://github.com/holocaustio/kehilot) portal — the OCR,
the processed knowledge graph, and the editorial overlays that revive Yizkor (memorial) books.

This repository is the **source of truth for data**. The app repo (`kehilot`) holds only code;
at runtime it reads a checkout of this repository. Keeping data separate lets the graph, OCR,
and human editorial revisions evolve — and be reviewed via pull requests — without redeploying
the application.

## Layout

Everything lives under `data/`, mirroring the path layout the application expects 1:1:

- `data/yizkor-books/**` — per-book OCR (`ocr.txt`), source metadata (`*.json`, `*.xml`).
  The raw source PDFs are **not** here: they are large (tens of GB) and the app never reads
  them, so they stay local to whoever runs the extraction pipeline.
- `data/processed/**` — the reviewed, evidence-bound pipeline output the public portal reads
  (extraction, adjudication, entity resolution, reading paths, the selected release).
- `data/editorial/**` — human editorial overlays, revisions, and published articles.
  The app's editorial workflow commits here (branch `editorial/live`, opened as PRs to `main`).

## How the app consumes it

The app resolves data through `lib/data-store.ts`:

- Locally, the app's own `./data` directory is the checkout, so development needs no setup.
- In production, set `KEHILOT_DATA_DIR` to a clone of this repo. Refresh it with `git pull`
  (via `refreshDataMirror()` on boot or a deploy/webhook) to pull data live.

## Reviewing editorial changes

Editorial edits and published articles arrive as commits on `editorial/live` and a rolling
pull request into `main`. **A PR here is a proposed revision to the public record** — merging it
is what makes an edit go live to readers on the next data refresh.
