\# Audit Stage

This file is the canonical stage playbook for the paper-spine orchestrator.

\## Purpose

Audit all PaperSpine outputs before declaring the workflow complete.

\## Required Checks

1\. Artifact completeness.
2\. Reference material workspace has \`source\_index.md\`.
3\. Motivation was user-confirmed after research.
4\. \`writing\_rationale\_matrix.md\` exists, is ordered, and covers whole-work
 framework + task-specific writing units.
5\. No append-only or shallow revision for substantive rewrite tasks.
6\. Logic transfer from original draft or materials.
7\. Claim support from user evidence.
8\. LaTeX citation, label, figure safety.
9\. \`citation\_support\_bank.md\` count, recency, quality, and Source Channel audit.
10\. Final LaTeX source; PDF when TeX available.
11\. Word output structurally valid by default; skip only when
 \`word\_output=none\` is explicit in config.
12\. Submission materials pass \`submission\_check.py\`.
13\. Translation coverage complete when \`translation\_package=zh\`.
14\. When \`translation\_package=zh\` and Word output is enabled,
 \`final\_paper/paper.zh.docx\` and \`word\_report.zh.md\` exist and pass. The
 \`translation\_zh/\` folder is an audit/intermediate package, not the final
 Chinese Word deliverable.

\## Scripts

\`\`\`bash
python scripts/integrity\_audit.py paper\_rewriting\_output --markdown --write
python scripts/artifact\_check.py paper\_rewriting\_output --markdown --write
python scripts/citation\_bank\_check.py paper\_rewriting\_output/citation\_support\_bank.md --markdown --write
python scripts/progress\_check.py paper\_rewriting\_output --markdown --write
python scripts/revision\_audit.py  --markdown
python scripts/structured\_review.py paper\_rewriting\_output --dispatch
python scripts/citation\_quality\_audit.py paper\_rewriting\_output --write
python scripts/latex\_guard.py  --bib  --markdown
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.docx --tex paper\_rewriting\_output/final\_paper/main.tex --markdown --output paper\_rewriting\_output/word\_report.md
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.zh.docx --tex paper\_rewriting\_output/final\_paper/main.tex --markdown --output paper\_rewriting\_output/word\_report.zh.md
python scripts/submission\_check.py paper\_rewriting\_output/submission\_package --fix-fonts --markdown --write
\`\`\`

\## Required Outputs

\- \`integrity\_audit.md\`, \`artifact\_check.md\`, \`revision\_audit.md\`
\- \`structured\_review.md\` (uses scene-aware reviewer personas from config; does
 not fabricate venue rules, only what the research stage or user provides),
 \`citation\_quality\_audit.md\`, \`logic\_transfer\_audit.md\`
\- \`submission\_package/submission\_check.md\` (when applicable)
\- \`final\_paper/paper.zh.docx\` and \`word\_report.zh.md\` when
 \`translation\_package=zh\`

Do not declare the task complete if required artifacts are missing, claims are
unsupported, translation is partial, the rationale matrix is generic, or the
final Chinese Word document is missing.

\## Output Directory Rules

The workflow root is \`paper\_rewriting\_output/\`. All artifacts must live inside
it. The following are hard errors that prevent completion:

\- \*\*No nested directories:\*\* Do not create \`paper\_rewriting\_output/\` inside
 \`paper\_rewriting\_output/\`. If a nested inner directory is detected, move all
 contents up one level and remove the inner directory.
\- \*\*No sibling final\_paper:\*\* \`final\_paper/\` must exist only inside
 \`paper\_rewriting\_output/\`, never as a sibling next to it. If both exist,
 remove the sibling copy outside \`paper\_rewriting\_output/\`.
\- \*\*No misplaced artifacts:\*\* \`writing\_rationale\_matrix.md\`,
 \`citation\_support\_bank.md\`, \`research\_dossier.md\`, and other workflow
 artifacts belong inside \`paper\_rewriting\_output/\`, not outside it.

\## Completion Hard Gate

Before declaring the workflow complete, run the checks below in order.
\`progress\_check.py --gate final\_audit\` is the authoritative hard gate: it
re-runs \`artifact\_check.py\`, \`citation\_bank\_check.py\`, \`integrity\_audit.py\`,
\`citation\_quality\_audit.py\`, the required \`word\_guard.py\` check, and — once
\`final\_paper/main.tex\` exists — \`latex\_guard.py\` and \`section\_economy\_check.py\`,
then fails on any non-zero exit code.
Do not treat existing report files as enough evidence of completion.

These last two read the manuscript body, not just report shapes:
\`latex\_guard.py\` fails literal-bracket citations that are not real \`\\cite\`
links and out-of-sync numbering; \`integrity\_audit.py\` fails writing-process /
meta-narrative language (supervisor or reviewer mentions, "reorganized the
paper", transcribed \`A -> B -> C\` plan chains) leaking into the prose; and
\`section\_economy\_check.py\` fails a top-level section count above the
applied-paper budget (4-6). A clean report file is not enough — the body must
pass.

\`\`\`bash
python scripts/artifact\_check.py paper\_rewriting\_output --markdown --write
python scripts/citation\_bank\_check.py paper\_rewriting\_output/citation\_support\_bank.md --markdown --write
python scripts/progress\_check.py paper\_rewriting\_output --gate final\_audit
python scripts/integrity\_audit.py paper\_rewriting\_output --markdown --write
python scripts/progress\_check.py paper\_rewriting\_output --markdown --write
\`\`\`

When \`word\_output\` is not explicitly \`none\` and \`output\_language\` is not \`zh\`,
also run:

\`\`\`bash
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.docx --markdown --output paper\_rewriting\_output/word\_report.md
\`\`\`

When \`translation\_package=zh\` or \`output\_language=zh\`, also run:

\`\`\`bash
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.zh.docx --markdown --output paper\_rewriting\_output/word\_report.zh.md
\`\`\`

When \`translation\_package=zh\`, also run and require PASS:

\`\`\`bash
python scripts/translate\_guard.py paper\_rewriting\_output --markdown --write
\`\`\`

The final Chinese Word file must be predominantly Chinese and free of visible
Markdown emphasis markers such as \`\*\*bold\*\*\` or \`\*italic\*\`. A \`.zh.docx\` file
that contains English body prose under a Chinese title is a failed translation
package.

You may declare completion only when \`progress\_check.py --gate final\_audit\`
exits 0, \`artifact\_check.py\` exits 0, final progress reports
\`is\_complete=true\`, no \`misplaced\_artifacts\` are reported, integrity audit has
no unresolved BLOCKER, and Word output is present and valid unless the user
explicitly opted out. If pandoc is unavailable, write BLOCKED/FAIL in
\`latex\_report.md\`; do not silently skip Word or claim the workflow is complete.

\## Anti-Pass-Through Rule

\*\*If \`artifact\_check.md\` reports Status: FAIL or Status: BLOCKED, the workflow
is not complete.\*\* Do not declare completion. Do not write \`progress.md\` with
\`is\_complete=true\`. Return to the failing upstream stage:

\- Missing artifacts → run that stage.
\- Content issues (weak rationale matrix, thin citation bank) → fix the
 artifact, then re-run \`artifact\_check.py\`.
\- Misplaced artifacts → move them into \`paper\_rewriting\_output/\`.

\*\*If \`citation\_bank\_check.md\` reports Status: FAIL, the citation support bank
is not qualified.\*\* The final audit must not pass until the bank is re-run and
all weak rows are strengthened with reference format + claim-support sentences.

\*\*If \`writing\_rationale\_matrix.md\` rows are too thin (generic cells, fewer than
8 rows, first-row framework missing), \`artifact\_check.py\` will report FAIL.\*\*
The progress gate will not clear until the matrix is rewritten with concrete
motivation, reference/SOTA, target-scene, evidence, and text-move anchors per
row.