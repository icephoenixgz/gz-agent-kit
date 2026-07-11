\# Resume / Continue From Checkpoint

PaperSpine supports resuming from the first incomplete stage when a prior run
was interrupted. Do \*\*not\*\* restart from scratch unless the user explicitly
asks for a clean run.

\## Anti-Skip Rule

\*\*No stage may be skipped.\*\* When a stage's artifacts are missing, that stage
MUST be executed before any later stage. Do not:
\- Hand-write a missing artifact to "fill the gap"
\- Patch a downstream file to work around a missing upstream artifact
\- Proceed with a "we'll fix it later" note
\- Skip a stage because the user seems in a hurry
\- Use \`generate\_artifacts.py\`, \`quick\_generate.py\`, \`mock\_artifacts.py\`, or
 any bulk script to create placeholder intermediate files instead of running
 the real research, citation, planning, writing, or audit stage

A missing artifact means the stage that should have produced it was not run.
Run that stage. This is non-negotiable.

\## Resume Loop

Resume is a loop, not a one-step patch:

1\. Run \`progress\_check.py paper\_rewriting\_output --markdown --write\`.
2\. Execute the reported \`next\_stage\` by reading its \`references/\*.md\` playbook.
3\. Run \`progress\_check.py paper\_rewriting\_output --gate \`.
4\. If the gate passes, run the full progress check again.
5\. Continue with the new \`next\_stage\` until \`final\_audit\` is complete.

Do not stop after fixing one missing stage unless:
\- the workflow is BLOCKED on user confirmation;
\- a required external tool is missing and the report states BLOCKED/FAIL;
\- the user explicitly asks you to pause.

\## Rules

1\. \*\*Before starting any workflow\*\*, run \`progress\_check.py\` against
 \`paper\_rewriting\_output/\`. Read the output (Markdown or JSON) to determine
 \`next\_stage\`.

2\. \*\*If \`next\_stage\` is \`intake\`\*\* and config already exists, verify the config
 is complete before re-entering intake. If config is valid, advance to the
 next stage.

3\. \*\*If \`next\_stage\` is \`motivation\_confirmation\` and status is \`BLOCKED\`:\*\*
 stop and present the existing \`motivation\_options\_after\_research.md\` to the
 user. Do not rewrite the motivation options. Wait for explicit user
 confirmation before writing \`confirmed\_motivation.md\`.

4\. \*\*For any other \`next\_stage\`\*\*, read the corresponding \`references/\*.md\`
 playbook and execute that stage. Do not re-run earlier stages whose
 artifacts already exist and are valid.

5\. \*\*When a stage completes\*\*, run \`progress\_check.py --gate \` to
 verify the stage's artifacts before moving to the next stage. If the gate
 fails, the stage is not complete — return to it.

6\. \*\*The \`progress.md\` file\*\* (written by \`progress\_check.py --write\`) is the
 authoritative resume map. Read it alongside the script output.

7\. \*\*Misplaced artifacts are not completion evidence.\*\* If \`final\_paper/\`,
 \`writing\_rationale\_matrix.md\`, \`citation\_support\_bank.md\`,
 \`translation\_zh/\`, or other workflow artifacts appear next to
 \`paper\_rewriting\_output/\` instead of inside it, treat the run as incomplete.
 Rebuild or move the artifacts under \`paper\_rewriting\_output/\`; do not declare
 completion from outer-directory files.

 \*\*Nested directories are a hard error.\*\* If \`paper\_rewriting\_output/\`
 contains another \`paper\_rewriting\_output/\` inside it, artifacts were written
 one level too deep. Move all contents up one level and remove the inner
 directory. Do NOT declare completion while a nested directory exists.

 \*\*Sibling final\_paper is a hard error.\*\* If \`final\_paper/\` exists both in
 the parent directory (sibling to \`paper\_rewriting\_output/\`) and inside
 \`paper\_rewriting\_output/\`, keep only the copy inside and remove the sibling.

8\. \*\*Word is required by default.\*\* If \`paper\_spine\_config.json\` does not set
 \`word\_output\`, treat it as \`docx\`. Only an explicit \`word\_output=none\`
 disables Word output.

9\. \*\*artifact\_check.md FAIL or BLOCKED blocks completion.\*\* If
 \`artifact\_check.md\` reports \`Status: FAIL\` or \`Status: BLOCKED\`, the
 workflow is not complete. Do not declare \`is\_complete=true\`. Return to the
 failing upstream stage (missing artifacts, weak rationale matrix, thin
 citation bank, or misplaced artifacts). Only when \`artifact\_check.py\`
 exits 0 and the progress report shows \`is\_complete=true\` may completion be
 declared.

10\. \*\*citation\_bank\_check FAIL blocks completion.\*\* If \`citation\_bank\_check.md\`
 reports \`Status: FAIL\`, the citation support bank is not qualified. Return
 to the citation stage and fix weak rows before proceeding.

\## Gate Script

\`\`\`bash
\# Resume check (full progress scan)
python scripts/progress\_check.py paper\_rewriting\_output --markdown --write

\# Stage-level gate (after completing a stage)
python scripts/progress\_check.py paper\_rewriting\_output --gate research
python scripts/progress\_check.py paper\_rewriting\_output --gate citation
python scripts/progress\_check.py paper\_rewriting\_output --gate planning
python scripts/progress\_check.py paper\_rewriting\_output --gate drafting
python scripts/progress\_check.py paper\_rewriting\_output --gate integrity\_audit
python scripts/progress\_check.py paper\_rewriting\_output --gate latex
python scripts/progress\_check.py paper\_rewriting\_output --gate word --require
python scripts/progress\_check.py paper\_rewriting\_output --gate final\_audit
\`\`\`

\## Restart (Clean Run)

Only when the user explicitly requests a restart, delete or rename the output
directory and begin from intake.