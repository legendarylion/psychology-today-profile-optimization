# Questionnaire to Psychology Today Field Map

Connects the intake questionnaire (`_ref/intake-questionnaire.md`) to the
Psychology Today profile fields. Use this in Mode B (build from intake) to know
which answers feed which field, and which limit each must respect. Limits are
authoritative in `limits.json`.

The questionnaire is intentionally multi-platform (Zencare, Zocdoc, Google
Business Profile, Private Practice Directory). This map covers the Psychology
Today subset.

| PT field | Box / Note label | Limit | Primary questionnaire source |
|---|---|---|---|
| Part 1 - Ideal Client | "What can I help you with?" | 640 | 2.3 ideal-client description; 2.2 "in clients' own words"; 2.2 issues known for. Lead the first 270 chars with the plain-language symptoms from 2.2. |
| Part 2 - Approach | "What's my approach?" | 360 | 2.5 "describe your approach in plain language"; 2.5 modalities; 2.3 what makes you different |
| Part 3 - Authority + CTA | "About me" | 360 | 2.5 Authority & Trust Assets (publications, media, certifications); 2.5 free-consult format/length; 2.5 service delivery/states |
| Top Specialties (note) | "Note on Top Specialties" | 400 | 2.2 issues known for; 2.5 primary focus areas; 2.3 niche. Pick differentiating filters over saturated ones. |
| Therapy Types (note) | "Note on Therapy Types" | 400 | 2.5 modalities + plain-language approach; 2.3 misconception you correct |
| Credentials (note) | "Note on Credentials" | 300 | 2.5 Identity & Credentials; licensure + supervision status; education; strongest single trust asset |
| Finances (note) | "Note on Finance" | 300 | 2.4 fees, payment options, packages, sliding scale; 2.4 "display fees publicly?" |
| Intro to new clients | "Intro to new clients" | 140 | 3.2 reassurance language; 2.3 words clients use; CTA preference from 3.3 |
| Tagline | "Tagline" | 160 | 2.3 differentiation in one line; 3-5 words clients use (2.3) |

## Cross-checks the map encodes

- **Licensure (2.5).** The questionnaire captures license type, number, state,
  and supervision status precisely because the Credentials note and PT's
  verification display must agree. Mismatch erodes trust. Verify on every
  engagement.
- **Telehealth states (2.5 logistics).** Drives the statewide telehealth
  visibility setting, often the biggest visibility lever for online-only
  clinicians. Confirm it is enabled.
- **Words to avoid (2.3).** Apply as a banned-terms filter across all copy in
  addition to the house no-dash rule.
- **Consult length (2.5).** Use one number everywhere on the profile; the
  questionnaire records format and length so the CTA is consistent.
