# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A single-file, zero-dependency dashboard for tracking the progress of legal/case
proposals ("phương án") **PC08** and **PC09**. The entire application — markup,
styles, data, and logic — lives in `index.html`. The UI language is Vietnamese.

There is no build step, no package manager, and no test suite. To run or test,
open `index.html` directly in any browser (it works fully offline).

## Architecture (all in `index.html`)

The page renders four sections, each driven by a `render*()` function called in
the `/* ─── Init ─── */` block at the bottom of the `<script>`:

- **KPIs** (`renderKPI`) → `#kpiRow`
- **Progress vs. targets** (`renderProgress`, helper `progressCard`) → `#progressGrid`
- **Trend / snapshots over time** (`renderSnaps`, `addSnapshot`) → `#snapTable`
- **Per-person detail table** (`renderPersonTable`) → `#personTable` / `#personFoot`

### Two distinct data layers — keep them separate

1. **Static source data** — the `people` array (hardcoded ~18 records, each with
   `total / signed / stamped / unsigned / pc09s / pc09d`) plus the `TARGET*` and
   `*_DATE` constants near the top of the script. This is edited in source.
   Aggregates are derived once into `tot` via `people.reduce(...)`.

2. **Mutable snapshot data** — `snapData`, persisted in `localStorage` under the
   key `pc08snaps`. Seeded from `BASELINE` (built from the static aggregates) on
   first load. The trend table is fully editable in the browser; every change
   calls `saveSnaps()` then re-renders. **This data is NOT in git** — it lives
   only in each user's browser.

### Key domain semantics (easy to get wrong)

- `signed` = "đã ký **chưa** đóng dấu" (signed but NOT yet stamped). It is a
  distinct bucket and is **never** rolled into `stamped`.
- `stamped` = "đã ký **và** đóng dấu" (signed AND stamped).
- `unsigned` = "chưa ký" (not signed). In `deltaChip`, an increase in `unsigned`
  is treated as *bad* (pass `invert=true`); for `signed`/`stamped` an increase is
  *good*.
- Targets: two deadlines (`TARGET1_DATE` 30/06/2026, `TARGET2_DATE` 14/10/2026).
  `TARGET2_PC08 = 1372 + 110` (base + "phát sinh"/additional). Per-week pacing
  comes from `weeksLeft(today, target)`.

## Conventions

- Plain vanilla HTML/CSS/JS — no frameworks, no external JS dependencies (only a
  Google Fonts `<link>`). Keep it dependency-free and single-file.
- Theming via CSS custom properties in `:root` (GitHub-dark palette). Reuse the
  existing `--bg/--surface/--accent/--green/...` variables and `.chip-*`,
  `.delta-*` classes rather than introducing new colors.
- Rendering is string-template `innerHTML` assignment; mutation handlers are
  inline `onchange`/`onclick` attributes that mutate `snapData[i]` then call
  `saveSnaps()` and re-render. Follow this pattern for new editable fields.
- When updating the underlying numbers, edit the `people` array (and `TARGET*`
  constants / `SNAPSHOT_DATE`) — do not duplicate totals; they are computed.
- Bump the version string in both `README.md` and the `<footer>` when shipping a
  meaningful change.

## Updating the dataset

New counting rounds are added at runtime via the "＋ Thêm thời điểm kiểm đếm"
button (stored in localStorage, per-browser). To change the canonical baseline
that ships with the file, edit the `people` array in `index.html`.
