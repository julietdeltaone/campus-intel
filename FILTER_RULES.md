# Campus Intel — Big-Ticket Filter Rules

How the weekly sweep decides what gets logged and what gets dropped. Rules are
explicit so classification is auditable. Anything matching no rule goes to the
review bucket — never silently dropped, never auto-included.

## Signal taxonomy
`new_program` · `tuition_change` · `leadership` · `notable` · `noise` (dropped)

## new_program → Tier 1 (chat alert + digest)
A credential-bearing offering that did not exist before: degree, major,
certificate, school/college. Patterns (case-insensitive) in title or lead:
"announces new", "launches new", "new degree", "new major", "new program",
"now offering", "begin offering", "approved by", "NYSED" + program.
Must name a credential (AAS, BA, BS, MA, MS, certificate, microcredential).
- New minors → review bucket (borderline).
- New courses, new course sections → noise.
- Worked example: SUNY Canton "Health Care Studies" AAS for Fall 2027
  (2026-10-05) = new_program, Tier 1, confirmed.

## tuition_change → Tier 1 (chat alert + digest)
- Tuition/fees page content hash changes week-over-week → verify the delta is an
  actual rate change (not a redesign or date rollover) before logging.
- News items matching "tuition" AND ("increase" | "decrease" | "freeze" |
  "rates" | "approved" | "vote") → review bucket first, classify on read.

## leadership → Tier 1 at Clarkson, Tier 2 elsewhere
- Org-chart diffs: the tracked charts/pages are already top-level, so ANY
  addition, removal, or title change in the tracked leadership list counts.
- News-based detection: person + title matching president | chancellor |
  provost | vice president | dean (any "dean of" / named dean). Departures count:
  "steps down", "retires", "named interim", "appointed", "joins as".
- Individual faculty hires, staff awards → noise.

## notable → Tier 2 (digest only)
Rankings ("ranked", "ranking", "best"), enrollment milestones, fundraising
records ("record $", "million" + gift/pledge), construction/groundbreaking,
accreditation actions, major partnerships, large grants ($1M+).

## noise → never logged
Club/org announcements, event invitations ("join us", "hosts", "you're invited",
"trunk or treat", open house), athletics game recaps and schedules, faculty/staff
Q&A profiles ("meet ...", "Q&A:"), student/faculty awards, department-level news,
"call for submissions", honor rolls.

## Review bucket protocol
1. Item matches no big-ticket rule and no noise rule → review bucket.
2. The weekly run's agent reads each review item and classifies it with a
   confirmed/inference chip.
3. Every review decision is appended to the log with its reason, so these rules
   improve over time. A pattern decided twice becomes a rule here.

## Dedupe
The same story appearing on a news index and a year archive (or across weeks)
is logged once, under its earliest observed date.
