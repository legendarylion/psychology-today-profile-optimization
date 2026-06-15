# Optimization Process (Playbook)

How to run a Psychology Today profile optimization from input to delivered copy.
The goal of every engagement: improve search visibility, first-impression
conversion, and trust consistency without erasing the clinician's voice.

## Inputs: two modes

An engagement starts from one of two input types. Both are valid; the steps
differ only at the start.

- **Mode A - Refine an existing profile.** The client has a live profile (or
  pasted bio). Capture the current copy verbatim into `source/`. The job is
  re-sequencing, tightening, and limit-fitting, not a ground-up rewrite. This
  was the Michael Lydon engagement.
- **Mode B - Build from intake.** The client has little or no existing copy.
  Use the filled intake questionnaire (`_ref/intake-questionnaire.md`) as the
  source. Map answers to fields via `questionnaire-to-pt-field-map.md`, then
  draft fresh copy.

In both modes, anything the client wrote in their own words (bio, "in your
clients' own words" answers, words they love/avoid) is the voice reference.
Preserve it.

## Steps

1. **Set up the client folder.** `clients/<slug>-<YYYY-MM-DD>/` with a
   `source/` subfolder for inputs (existing profile, filled questionnaire,
   headshot notes) and the deliverable at the top level.
2. **Gather the raw material.** Mode A: paste the current profile into
   `source/`. Mode B: confirm the questionnaire is complete enough (sections
   2.2, 2.3, 2.5, 2.4, and 3.2 are the load-bearing ones for a profile).
3. **Findings pass.** Identify high-impact issues. The recurring ones:
   - opening line buries the hook (first 270 chars of Box 1 are the search preview);
   - Top Specialties chase saturated filters instead of the client's real differentiation;
   - conceptual language where plain symptom/outcome language would convert better;
   - inconsistent consult length / other trust contradictions;
   - licensure display vs. headline mismatch (we check this every time);
   - underused authority assets (publications, media, certifications).
4. **Draft the copy** into a copy of `_templates/optimized-profile-template.md`.
   Write each block as a single unwrapped paragraph so it pastes cleanly. Aim
   for roughly 80% of each limit (see `limits.json`) so nothing truncates on
   small screens; never exceed 100%.
5. **Verify limits and style.** Run the checker:
   ```
   python3 tools/check_limits.py clients/<slug>-<date>/optimized-profile.md --update
   python3 tools/check_limits.py clients/<slug>-<date>/optimized-profile.md
   ```
   The first sets the counts; the second must report PASSED (exit 0). It also
   blocks em/en dashes, which are house-style violations.
6. **Punch list + guidance.** Add the smaller fixes (typos, specialty swaps,
   telehealth setting, group-session description), video notes, and the
   implementation checklist. Keep these separate from the paste-ready copy.
7. **Generate the client document.** The `.md` is the internal source of
   truth; the client gets a formatted document. Build it with:
   ```
   python3 tools/build_docx.py clients/<slug>-<date>/optimized-profile.md
   ```
   This writes a namespaced deliverable into the client folder, e.g.
   `michael-lydon-optimized-profile-2026-06-15-123557.docx`, with each copy
   block in its own shaded, bordered box and the field name + live count as a
   caption above it. The datetimestamp means revision runs never overwrite an
   earlier delivery. The build refuses to run on over-limit or dash-dirty copy,
   so it doubles as a final gate.
8. **Deliver.** Upload the `.docx` to Google Drive, open it as a Google Doc,
   and share the link. The boxes survive the conversion as tables, so the
   client can click a box, select all, and paste it straight into the matching
   Psychology Today field without grabbing a label or count.

## Hard rules

- Every copy block fits its Psychology Today limit. The checker is the gate;
  do not deliver on a FAIL.
- No em dashes or en dashes anywhere in client-facing copy. Plain hyphens only.
- `limits.json` is the single source of truth for limits. If Psychology Today
  changes a limit, update `limits.json` and re-run the checker on past
  deliverables; do not hardcode numbers elsewhere.
- Preserve the clinician's voice. Re-sequence and tighten before rewriting.
