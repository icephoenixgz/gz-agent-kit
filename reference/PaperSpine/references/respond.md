\# Review Response Workflow

Use this stage when the user has reviewer comments and needs a revision
response package. Do \*\*not\*\* create a separate skill — this is routed from
the main \`paper-spine\` orchestrator.

\## Output Directory

\`\`\`
paper\_rewriting\_output/review\_response/
\`\`\`

\## Inputs

\- Reviewer comments file or user-pasted text
\- Original manuscript: \`final\_paper/main.tex\`
\- Supporting artifacts: \`writing\_rationale\_matrix.md\`, \`evidence\_bank.md\`,
 \`claim\_register.md\` (read when available)

\## Comment Extraction

If reviewer comments are not already numbered, extract and assign IDs:

\- \`R1.C1\`, \`R1.C2\`, \`R2.C1\`, etc. (\`R\` = Reviewer, \`C\` = Comment)
\- Present the extracted list to the user for confirmation before proceeding.

\## Required Outputs

\### 1\. \`reviewer\_comments\_extracted.md\`

Numbered list of every reviewer comment with stable Comment IDs.

\### 2\. \`response\_matrix.md\`

\| Comment ID \| Reviewer \| Original Comment \| Issue Type \| Required Action \| Manuscript Change \| Evidence / Source \| Response Draft \| Status \|
\|\-\-\-\|\-\-\-\|\-\-\-\|\-\-\-\|\-\-\-\|\-\-\-\|\-\-\-\|\-\-\-\|\-\-\-\|

\- \*\*Comment ID\*\*: \`R1.C1\`, etc.
\- \*\*Issue Type\*\*: \`major\` / \`minor\` / \`clarification\` / \`format\`
\- \*\*Status\*\*: \`draft\` / \`final\` / \`needs-author\`

\### 3\. \`response\_letter.md\`

Point-by-point response letter addressed to the editor/reviewers. Each
comment ID must appear. Polite, specific, and locatable in the manuscript.

\### 4\. \`revision\_change\_log.md\`

Summary of every revision made, with manuscript line/section references.

\### 5\. Revised manuscript

Either \`revised\_manuscript.md\` or a note that changes have been applied to
\`final\_paper/main.tex\`.

\## Rules

\- Every reviewer comment must receive an individual response. No omissions.
\- Responses must be polite, specific, and traceable to a manuscript change.
\- Do \*\*not\*\* fabricate new experiments, data, statistics, author info, or
 reviewer comments.
\- When user data is needed, use explicit placeholders:
 \`\[NEEDS USER DATA: \]\`
 \`\[AUTHOR CONFIRMATION REQUIRED: \]\`
\- If a comment cannot be adopted, explain why and offer an alternative.
\- All changes must be traceable to the original manuscript, \`evidence\_bank\`,
 \`claim\_register\`, or explicit user supplements.
\- Do \*\*not\*\* silently pass unresolved comments to appear complete.

\## Verification

\`\`\`bash
python scripts/respond\_check.py paper\_rewriting\_output/review\_response --markdown --write
\`\`\`

Produces \`review\_response/respond\_check.md\`. Fix all FAIL findings before
delivery.