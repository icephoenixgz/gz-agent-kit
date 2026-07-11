\# Translate Stage

This file is the canonical stage playbook for the paper-spine orchestrator.

\## Purpose

Produce the complete \`translation\_zh/\` package when \`output\_language=en\` and
\`translation\_package=zh\`. Every required file must be translated; partial
translation is a failed output.

Important: \`translation\_zh/\` is the Chinese translation audit/intermediate
package. It is not the final user-facing Chinese document. When Word output is
enabled, the final Chinese deliverable must also be generated as one Word file:

\- \`paper\_rewriting\_output/final\_paper/paper.zh.docx\`
\- \`paper\_rewriting\_output/word\_report.zh.md\`

Do not report "Chinese translation: translation\_zh/ - 10 files" as the final
Chinese doc deliverable. The user-facing result is \`paper.zh.docx\`.

\## Three-Phase Flow

\### Phase 1 - Inventory

List every file to translate. Write \`translation\_zh/manifest.md\`. \`translate\_guard.py\`
demands the exact set below (every file lives under \`translation\_zh/\`); a missing
file is a BLOCKER.

Common files (required for both workflows):

\- \`manifest.md\`
\- \`translation\_coverage.md\`
\- \`paper\_spine\_config.zh.md\`
\- \`source\_map.zh.md\`
\- \`reference\_materials/source\_index.zh.md\`
\- \`research\_dossier.zh.md\`
\- \`exemplar\_learning\_dossier.zh.md\`
\- \`style\_profile.zh.md\`
\- \`sota\_gap\_map.zh.md\`
\- \`motivation\_options\_after\_research.zh.md\`
\- \`confirmed\_motivation.zh.md\`
\- \`section\_blueprints.zh.md\`
\- \`writing\_rationale\_matrix.zh.md\`
\- \`citation\_support\_bank.zh.md\`
\- \`final\_structure.zh.md\`
\- \`final\_paper.zh.md\`
\- \`full\_paper\_translation.zh.md\`
\- \`latex\_report.zh.md\`
\- \`final\_artifact\_manifest.zh.md\`
\- \`artifact\_check.zh.md\`

Additional files for the \`rewrite\_existing\` workflow:

\- \`original\_logic\_map.zh.md\`
\- \`rewrite\_matrix.zh.md\`
\- \`logic\_transfer\_audit.zh.md\`

Additional files for the \`build\_from\_materials\` workflow:

\- \`source\_inventory.zh.md\`
\- \`evidence\_bank.zh.md\`
\- \`figure\_asset\_map.zh.md\`
\- \`claim\_register.zh.md\`

\### Phase 2 - Translate

\- Plain prose: translate full text; preserve LaTeX keys, labels, equations, URLs.
\- Large tabular files: translate every row and cell; no summary.
\- \`full\_paper\_translation.zh.md\`: title, abstract, every section, captions,
 tables, conclusion, appendix.

\### Phase 3 - Final Chinese Word Document

After \`translation\_zh/full\_paper\_translation.zh.md\` is complete, convert it into
the final user-facing Chinese Word document:

\`\`\`bash
pandoc paper\_rewriting\_output/translation\_zh/full\_paper\_translation.zh.md \
 -o paper\_rewriting\_output/final\_paper/paper.zh.docx
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.zh.docx \
 --markdown --output paper\_rewriting\_output/word\_report.zh.md
\`\`\`

If pandoc is unavailable while Word output is required, write BLOCKED/FAIL in
the relevant report and do not claim the Chinese deliverable is complete.

\### Phase 4 - Verify

\`\`\`bash
python scripts/translate\_guard.py paper\_rewriting\_output --markdown --write
python scripts/progress\_check.py paper\_rewriting\_output --gate word --require
\`\`\`

Require PASS. Write \`translation\_coverage.md\`.

\## Integration

Called after LaTeX and before audit. The orchestrator requires translate guard
to PASS before audit begins. When Word output is enabled, the workflow is not
complete until \`final\_paper/paper.zh.docx\` and \`word\_report.zh.md\` exist.