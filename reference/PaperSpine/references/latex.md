\# LaTeX Stage

This file is the canonical stage playbook for the paper-spine orchestrator.

\## Purpose

Assemble the LaTeX project, compile PDF when possible, and produce Word output.
Word (.docx) is a standard required artifact, not optional. Do not change
manuscript logic during assembly.

For a section-by-section, template-first conversion (copy the base \`.tex\`,
\`Edit\` only prose paragraphs, preserve preamble / floats / equations /
\`\\maketitle\` / bibliography commands) and the compile-and-fix + content-integrity
steps, follow \`references/round3-latex-polish.md\` then
\`references/round4-template-integration.md\`. They also walk the proper citation
mechanism — \`\\cite\` + \`\\bibliographystyle\`/\`\\bibliography\` resolved by bibtex —
which is exactly the linkage \`latex\_guard.py\` now enforces (see the citation
hard rule below).

\## Required Outputs

\- \`final\_paper/main.tex\`
\- \`final\_paper/main.pdf\` (compiled source PDF when TeX engine is available)
\- \`final\_paper/paper.pdf\` (must be a current copy of \`main.pdf\`)
\- \`final\_paper/paper.docx\` + \`word\_report.md\`
\- \`final\_paper/paper.zh.docx\` + \`word\_report.zh.md\` when \`translation\_package=zh\`
\- \`latex\_report.md\`
\- \`final\_artifact\_manifest.md\`

\## Scripts

\`\`\`bash
python scripts/latex\_guard.py paper\_rewriting\_output/final\_paper/main.tex --markdown
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.docx --tex paper\_rewriting\_output/final\_paper/main.tex --language en --fix-fonts
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.docx --tex paper\_rewriting\_output/final\_paper/main.tex --language en --markdown --output paper\_rewriting\_output/word\_report.md
\`\`\`

\## Key Rules

\*\*PDF alias (hard rule):\*\* after compiling \`final\_paper/main.pdf\`, copy it to
\`final\_paper/paper.pdf\` in the same run. \`paper.pdf\` must match \`main.pdf\`;
never leave an older \`paper.pdf\` beside a newer \`main.pdf\`.
\`artifact\_check.py\` fails stale or mismatched \`paper.pdf\`.

\*\*Citation mechanism (hard rule):\*\* Every in-text citation must be a real
\`\\cite{key}\` linked to a bibliography entry — either \`\\bibliographystyle{unsrt}\`
(or \`plain\`/\`ieeetr\`) + \`\\bibliography{references.bib}\`, or a \`thebibliography\`
block whose \`\\bibitem{key}\` entries are reached by \`\\cite{key}\`. Never type the
bracket number as literal text: a hand-typed \`\[1\]\` is inert and links to nothing
in either the PDF or the .docx, and the numbering silently desyncs if the
reference list reorders. A numeric \`bibliographystyle\`/CSL still renders as \`\[1\]\`
or \`\[3,12,13\]\`, so the visible plain-numeric style is preserved. Author-year
citations and extra-parenthesized numeric citations such as \`(\[15\])\` are
forbidden. Do not use superscript for these citations unless the target journal
explicitly requires it. \`latex\_guard.py\` fails literal-bracket citations that
have no \`\\cite\` and flags numbering that exceeds the reference-entry count.

\*\*Title (hard rule):\*\* \`main.tex\` must contain \`\\title{...}\` (with the paper's
title) and \`\\maketitle\` after \`\\begin{document}\`. Word output must begin with
the paper title on the first page, not Abstract, Keywords, Introduction, or
body paragraphs. \`latex\_guard.py\` checks the TeX source; \`word\_guard.py\`
checks the .docx.

\- Preserve citation keys and labels.
\- Copy approved images into \`figures/\` with stable labels.
\- For Chinese: prefer XeLaTeX + CJK-capable template.
\- If no TeX engine: keep \`.tex\`, record skipped compilation.
\- If compilation fails: keep \`.tex\`, write first fatal error, do not claim pass.
\- Word output is mandatory by default. If \`word\_output\` is missing, treat it as
 \`docx\`. Only explicit \`word\_output=none\` opts out.
\- If pandoc is unavailable while Word is required, write BLOCKED/FAIL in
 \`latex\_report.md\`, keep the workflow incomplete, and do not silently skip
 Word.

\## English Word Output

From \`final\_paper/\`:

\`\`\`bash
pandoc main.tex -o paper.docx --from latex --to docx \
 --resource-path=. --extract-media=./media \
 --number-sections --citeproc --bibliography=references.bib
\`\`\`

Flatten \`\\input\`/\`\\include\` with \`latexpand\` first. Expand or remove
\`\\newcommand\` macros. Verify tables, citations, figures after conversion.

After conversion, run \`word\_guard.py --fix-fonts\` first, then run
\`word\_guard.py --markdown --output ...\` and require PASS before proceeding.
English Word must use Times New Roman in the default/body/title styles and
theme fonts; do not rely on pandoc's default Office theme.

\`\`\`bash
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.docx \
 --tex paper\_rewriting\_output/final\_paper/main.tex \
 --language en --fix-fonts
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.docx \
 --tex paper\_rewriting\_output/final\_paper/main.tex \
 --language en --markdown --output paper\_rewriting\_output/word\_report.md
\`\`\`

If numbered headings render as \`1Introduction\` or \`2Methods\`, regenerate or
repair the Word file so headings read \`1 Introduction\`, \`2 Methods\`, etc.
\`word\_guard.py\` fails glued English heading numbers.

\## Final Chinese Word Output

When \`translation\_package=zh\` and \`word\_output\` is not explicitly \`none\`, the
final Chinese deliverable is a single Word document, not a folder of Markdown
files:

\- Required final file: \`paper\_rewriting\_output/final\_paper/paper.zh.docx\`
\- Required check report: \`paper\_rewriting\_output/word\_report.zh.md\`

Generate it from \`translation\_zh/full\_paper\_translation.zh.md\` after the
translation stage:

\`\`\`bash
pandoc paper\_rewriting\_output/translation\_zh/full\_paper\_translation.zh.md \
 -o paper\_rewriting\_output/final\_paper/paper.zh.docx
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.zh.docx \
 --tex paper\_rewriting\_output/final\_paper/main.tex \
 --language zh --fix-fonts
python scripts/word\_guard.py paper\_rewriting\_output/final\_paper/paper.zh.docx \
 --tex paper\_rewriting\_output/final\_paper/main.tex \
 --language zh --markdown --output paper\_rewriting\_output/word\_report.zh.md
\`\`\`

\`translation\_zh/\` remains the translation audit/intermediate package. Do not
list it as the only Chinese deliverable.
Chinese Word must use SimSun/宋体 for East Asian text and Times New Roman for
Latin text. If the font gate fails, repair the docx and re-run the report.

\*\*Chinese abstract heading:\*\* In a Chinese \`main.tex\`, author the abstract as
\`\\section\*{摘要}\` followed by the abstract paragraph rather than the LaTeX
\`abstract\` environment. pandoc renders \`\\begin{abstract}\` as an English
"Abstract" heading in the .docx even for a Chinese paper (the \`lang\` variable
does not localize it); \`\\section\*{摘要}\` produces 摘要 in both the ctex PDF and
the Word file.