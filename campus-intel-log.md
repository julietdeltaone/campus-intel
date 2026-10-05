# Campus Intel event log

Append-only. Each `## YYYY-MM-DD` section's FIRST pipe table is the structured
event table (`Date | School | Signal | Tier | Headline | URL | Status`), parsed by
`build_json.py` into `campus-intel.json`. Never edit the JSON by hand.

Signal taxonomy: `new_program` · `tuition_change` · `leadership` · `notable`.
Status: `confirmed` (verified against a primary source) or `inference` (needs a
second look). Noise is never logged. See `FILTER_RULES.md`.

## 2026-10-05 — baseline established

Baseline inventories captured for all four schools (news listings, program lists,
leadership, tuition pages + hashes) in `hidden_files/baselines/*.json`. Raw page
snapshots in `hidden_files/snapshots/<school>/`. Two Tier-1 items surfaced during
baseline construction and are logged below; the baseline itself sent no alerts.

| Date | School | Signal | Tier | Headline | URL | Status |
|---|---|---|---|---|---|---|
| 2026-10-05 | suny-canton | new_program | 1 | SUNY Canton announces new Health Care Studies AAS for Fall 2027 (21st associate degree; first of at least three new programs) | https://www.canton.edu/news/2026/healthcare.php | confirmed |
| 2026-10-05 | clarkson | new_program | 1 | Clarkson launching new BS in Neuroscience (interdisciplinary; tracks in cognitive science, neurobiology, computational neuroscience) | https://www.clarkson.edu/new-neuroscience-major | confirmed |

Notes:
- Clarkson Neuroscience: program page is live on clarkson.edu and advertised on
  the homepage, but it does not yet appear in Clarkson's official program
  listings — announcement date unverified; 2026-10-05 is first observed date.
- Canton HVAC Trades AOS was flagged as possibly new during baseline capture;
  verified NOT new (announced 2019, began Fall 2019). Not logged.
- Known baseline gaps: Potsdam programs list is the 2022-2023 archived catalog
  (current 2025-2026 not located); SLU leadership limited to president + one VP
  (detailed org chart is login-walled); several news article URLs unresolvable
  via browser outlinks — weekly runs should parse hrefs from raw HTML.
