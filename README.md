# Campus Intel

Weekly intel sweep over the four North Country universities — **Clarkson**,
**SUNY Canton**, **SUNY Potsdam**, **St. Lawrence** — tracking new programs,
leadership/org-chart changes, notable news, and tuition moves.

Change-only reporting. Big-ticket items surface; campus-club noise is filtered out.

## What's here

- **`campus-intel-log.md`** — the append-only typed event log. This is the source
  of truth. Each dated section's first table is the structured event table
  (`Date | School | Signal | Tier | Headline | URL | Status`).
- **`campus-intel.json`** — generated from the log (never hand-edited).
- **`FILTER_RULES.md`** — how the sweep decides what counts: the signal taxonomy
  (`new_program`, `tuition_change`, `leadership`, `notable`), the noise list,
  and the review-bucket protocol for ambiguous items.
- **`sources.json`** — the monitored source URLs per school, with per-source notes.
- **`baselines/`** — the 2026-10-05 baseline inventories (news listings, program
  lists, leadership, tuition pages + content hashes) that weekly diffs compare
  against.
- **`snapshots/`** — raw page snapshots backing the baselines.

## How it runs

A weekly job fetches each source page, hashes the content, and diffs against the
previous snapshot. New items are classified against `FILTER_RULES.md`; Tier-1
items (new programs, tuition changes, Clarkson leadership moves) trigger an
immediate alert, everything else lands in a Monday digest email. Quiet schools
collapse to a single count line.

No RSS feeds exist at any of the four schools — all detection is snapshot-and-diff
of public pages, fetched politely once a week from signed-out sessions.
