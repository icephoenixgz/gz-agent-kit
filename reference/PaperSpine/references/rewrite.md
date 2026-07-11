\# Rewrite Stage

This file is the canonical stage playbook for the paper-spine orchestrator.

\## Purpose

Substantively rewrite an existing manuscript from confirmed motivation, research
outputs, and a paragraph-level writing rationale matrix.

\## Prerequisites

\- \`paper\_spine\_config.json\`
\- User draft from \`draft\_path\`
\- Research outputs: \`research\_dossier.md\`, \`exemplar\_learning\_dossier.md\`,
 \`style\_profile.md\`, \`sota\_gap\_map.md\`
\- \`citation\_support\_bank.md\`
\- \`confirmed\_motivation.md\`

If any prerequisite is missing, return to the owning stage.

\## Humanize Tier

If \`paper\_spine\_config.json\` has \`humanize\_tier\` set to \`light\`, \`medium\`, or
\`heavy\`, read \`references/humanize.md\` and apply tier-specific constraints
during all prose generation.

\## Required Outputs

\- \`original\_logic\_map.md\` - map the existing manuscript in order
\- \`evidence\_bank.md\`
\- \`section\_blueprints.md\`
\- \`writing\_rationale\_matrix.md\` - the rewrite plan
\- \`rewrite\_matrix.md\`
\- \`logic\_transfer\_audit.md\`
\- Revised manuscript

\## Writing Rationale Matrix

\| Row ID \| Manuscript Unit \| Original Problem or Planned Function \| Motivation Link \| Reference/SOTA Pattern Learned \| Target Scene or Venue Norm \| User Evidence or Citation Anchor \| Planned Change \| Final Text Check \|
\|---\|---\|---\|---\|---\|---\|---\|---\|---\|

First row: deeply justify the whole-work framework. Each subsequent row must
teach why this writing move is better.

Before drafting, read \`references/writing-rationale-matrix.md\` and apply its
full depth rules. Every non-trivial row must include concrete anchors from
confirmed motivation, SOTA/example pattern, target scene, evidence/citation,
and the planned text move. After drafting, every \`Final Text Check\` value must
start with \`PASS\` or \`FAIL\`; do not write vague notes such as "done" or only a
section location.

\## Rewrite Rules

\- Rewrite from the matrix, not by appending to old paragraphs.
\- Preserve LaTeX commands, labels, citations, equations, figures, tables.
\- Use \`output\_language\` from config.
\- Select citations sentence by sentence from \`citation\_support\_bank.md\`.
\- \`rewrite\_matrix.md\` maps original to final units, classifying each change.

For a deeper, literature-informed pass — motivation-thread extraction,
move-guided section rewrite, structural-coherence pass, and a numerical /
cross-section motivation audit — apply the staged method in
\`references/round1-literature-revision.md\`.

\## Pre-LaTeX Gate

\`\`\`bash
python scripts/integrity\_audit.py paper\_rewriting\_output --markdown --write
python scripts/structured\_review.py paper\_rewriting\_output --dispatch
\`\`\`

After dispatch, launch three parallel review sub-agents per \`review\_prompts/dispatch.md\`.
Validate independence with \`structured\_review.py --validate review\_prompts\`.