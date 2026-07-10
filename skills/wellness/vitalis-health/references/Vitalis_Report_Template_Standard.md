# Vitalis Report Template Standard

Updated: 2026-04-08

## Purpose
Canonical structure/style reference for future full integrated Vitalis HTML reports.

This standard is based on the cleaned-up Dave integrated report structure and preferred styling as of 2026-04-08.

## Use this for
- full integrated longitudinal HTML reports
- main Vitalis patient reports

Do not use this file for the separate one-page user or clinician handoff summaries.

## Visual standard
- Keep the current premium dark/light visual system
- Keep the cleaner simplified header format
- Retain:
  - title text
  - theme toggle button
  - print / save PDF button
- Do not include:
  - large framed top strip
  - decorative logo
  - extra hero framing above the actual title
Unless the user explicitly asks for a more decorative header.

## Structural standard
Future full reports should follow the same broad structure used in the cleaned-up Dave report:

1. Title / short subtitle
2. Executive summary
3. Key dashboard cards
4. Longitudinal charts / trend visuals where relevant
5. Interpretation by system
   - cardiovascular / lipids
   - liver / metabolic
   - sleep / recovery
   - gut / hormone / body composition as relevant
6. Practical action plan
7. Dedicated nutrition section when clinically relevant
8. Formal structured protocol
9. Monitoring and unresolved items
10. Doctor-ready brief / summary section where useful

## Mandatory content rule
For cardiometabolic, liver-fat, alcohol-related, triglyceride, LDL/ApoB, body-composition, or gut-related cases, nutrition must appear as its own explicit section. Do not bury it under supplements, GLP-1s, peptides, or generic lifestyle text.

## Canonical live reference
The styling and structure target were taken from the cleaned-up local report:
- `Vitalis_Exports/Vitalis_Report_Dave_2026-04-06.html`

That file is gitignored because it is a generated export, so use this document as the tracked repo reference.
