# Psychology Today Profile Optimization

A repeatable service for optimizing therapist and counselor profiles on the
Psychology Today directory. The goal of each engagement is to improve three
things at once without erasing the clinician's voice:

1. **Search visibility** - appearing in the right directory filters and
   ranking for the terms real seekers type.
2. **First-impression conversion** - making the search-result preview and the
   top of the profile earn the click and the inquiry.
3. **Trust consistency** - removing the small contradictions (mismatched
   consult lengths, typos, unexplained options) that quietly erode confidence
   at the moment someone decides to reach out.

## What an engagement produces

A complete, paste-ready optimization package delivered as a single document:

- A short list of key findings (positioning, specialty selection, language,
  trust gaps).
- A rewritten three-part personal statement.
- Rewrites of the supporting note fields (Specialties/Expertise, Treatment
  Approach, Qualifications).
- A punch list of smaller fixes (typos, consult-length standardization,
  specialty swaps, telehealth settings).
- Video and implementation guidance.

Every block of client-facing copy must fit inside Psychology Today's character
limits **before** delivery. Exceeding a limit causes the platform to truncate
the text mid-sentence on the live profile, which is the exact problem this
project exists to prevent.

## Psychology Today character limits

Source: https://reframepractice.com/answers/psychology-today/best-psychology-today-profiles
(confirmed current as of the April 2026 version of that guide).

### Personal statement boxes

| Field | Box label | Limit |
|---|---|---|
| Part 1 - Ideal Client | "What can I help you with?" | 640 |
| Part 2 - Approach | "What's my approach?" | 360 |
| Part 3 - About Me / Authority + CTA | "About me" | 360 |

- Total cap across all three boxes: **1,360 characters**.
- The **first 270 characters of Box 1** appear as the directory search-result
  preview, so the strongest symptom keywords and hook belong up front.

### Structured note fields

| Field | Limit |
|---|---|
| Intro to new clients | 140 |
| Note on Finance | 300 |
| Note on Credentials (Qualifications) | 300 |
| Note on Top Specialties | 400 |
| Note on Therapy Types (Treatment Approach) | 400 |

### Other

| Field | Limit |
|---|---|
| Tagline | 160 |

### Drafting rule of thumb

The guide recommends writing to roughly **80% of each limit** so copy does not
truncate on smaller screens. Treat the numbers above as hard ceilings and the
80% figure as the comfort target. `limits.json` is the single source of truth
for the numbers; the checker reads from it, so update it there if PT changes a
limit. Never eyeball length: run the checker before delivery.

## Running an engagement

See `PROCESS.md` for the full playbook. In short:

1. Copy `_templates/optimized-profile-template.md` into the client folder.
2. Draft each block (refine an existing profile, or build from the intake
   questionnaire using `questionnaire-to-pt-field-map.md`).
3. Verify and set counts:
   ```
   python3 tools/check_limits.py clients/<slug>-<date>/optimized-profile.md --update
   python3 tools/check_limits.py clients/<slug>-<date>/optimized-profile.md
   ```
   The second run must report PASSED. It also blocks em/en dashes.
4. Generate the client document and deliver:
   ```
   python3 tools/build_docx.py clients/<slug>-<date>/optimized-profile.md
   ```
   This writes a namespaced, datetimestamped `.docx` into the client folder
   (e.g. `michael-lydon-optimized-profile-2026-06-15-123557.docx`) so revision
   runs never overwrite an earlier delivery. Upload it to Google Drive, open it
   as a Google Doc, and share the link. Each copy block is a boxed table the
   client can copy cleanly.

## Setup

```
pip install -r requirements.txt
```

## Repo layout

- `limits.json` - single source of truth for PT field character limits.
- `tools/check_limits.py` - verifies a deliverable fits limits and is dash-clean.
- `tools/build_docx.py` - builds the client-facing boxed `.docx` from the `.md`.
- `requirements.txt` - Python dependencies (`python-docx`).
- `PROCESS.md` - the optimization playbook (two input modes, steps, hard rules).
- `questionnaire-to-pt-field-map.md` - maps intake answers to PT fields.
- `_templates/` - blank, paste-ready deliverable template.
- `_ref/` - shared source material (the intake questionnaire).
- `clients/<slug>-<YYYY-MM-DD>/` - per engagement: `source/` inputs, the
  `optimized-profile.md` working file, and one or more namespaced
  `<slug>-optimized-profile-<datetimestamp>.docx` deliverables (git-ignored).
