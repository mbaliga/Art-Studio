# Art-Studio — multi-platform porting note

> Part of the constellation-wide porting program (`Personal-Tracker/PORTING_PROGRAM.md`, 2026-10-06).
> Status: **PLAN — nothing in this note has been built or run.** This is a disposition note, not a
> full plan, because the repo has no source to port. Evidence label for every claim: `PLAN`; the
> product-level claim is `NOT-APPLICABLE (README-only repo, no source)`.

## 1. What this repo is

`README.md` is the only tracked file: a title and one line of intent, "An open source system for art
studios presentation and management". The history is one commit (`8283ca7`, "Initial commit"). There
is no source, build file, CI workflow, licence file, `CLAUDE.md` or state file, and no stack has been
chosen, so the stack, size and test fields of a full plan are empty. Measured on 2026-10-06 with
`git ls-files` (1 file, 2 lines). Public on GitHub as `mbaliga/Art-Studio`.

## 2. Disposition by target (owner's order)

| Target | Feasibility | Approach | Blockers | Effort (eng-weeks, estimate) | Evidence today |
|---|---|---|---|---|---|
| Ubuntu Touch | not-applicable | Nothing to port; no source | none until a product exists | 0 | PLAN |
| Linux desktop | not-applicable | Nothing to port; no source | none until a product exists | 0 | PLAN |
| iOS / iPadOS | not-applicable | Nothing to port; no source | none until a product exists | 0 | PLAN |
| macOS | not-applicable | Nothing to port; no source | none until a product exists | 0 | PLAN |
| Windows | not-applicable | Nothing to port; no source | none until a product exists | 0 | PLAN |

There is no reframe either: a reframe needs a product to reshape, and none exists. Nothing here is a
port of anything, and nothing here claims to work on any device.

## 3. Tier and sequencing

Tier **skip**, as in the program's section 5 row (shared with `LG-Gear-VR-port`: README-only, public,
nothing to port, gate none). The repo joins no wave in section 7 and has no repo-local gate. It
consumes no shared-foundation item (F1 to F12) and provides none; no other repo needs anything from it.

## 4. If it is ever built

A full plan is written then, from the program's plan template, and replaces this note. What would
already bind it, by the program and not by any repo document (the repo has no invariants of its own):

- **Framework law (R8, section 4.6).** Kotlin + Compose goes through Kotlin Multiplatform + Compose
  Multiplatform; a web app is PWA first, then Tauri 2 (desktop) or Capacitor 8 (iOS), never both;
  Python stays Python; Godot uses its export templates; Ubuntu Touch is Click + QML or a webapp
  container. No Flutter, Electron or React Native rewrite. Which row applies depends on whether
  "presentation and management" becomes a website or an app, which is unknown today.
- **Directives (section 1).** I-1 no telemetry in an app (websites are pending OQ-18); I-2 on-device
  by default, cloud opt-in and marked; I-4 environment honesty; I-5 plain files. I-3 (colour never
  alone) binds Hyle consumers; whether it would bind this repo is unknown until it picks a design
  system (OQ-26 covers the non-Hyle repos, OQ-29 the undecided ones).
- **Program rules.** R1 to R4 (disjoint directories, existing gate stays green, new CI workflow files
  only, pure core first), R6 (nothing released, nothing stored on PRs), R11 (no click, Flatpak,
  bundle, MSI or winget identifier before a NAMES.md row), R12 (a reframe is labelled as one).

## 5. Open questions for the owner

None raised by this note; no program OQ (section 8) gates this row or changes this disposition.

## 6. Sources read

`README.md`; `git log` and `git ls-files` of this checkout; `Personal-Tracker/PORTING_PROGRAM.md`
sections 0 to 3, 4.6, this repo's section 5 row, and sections 6, 7 and 8.
