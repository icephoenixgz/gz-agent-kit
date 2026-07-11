\# Intake Stage

This file is the canonical stage playbook for the paper-spine orchestrator.

\## Purpose

Collect workflow options and write validated configuration before any substantive work.

\## Required Output

\- \`paper\_rewriting\_output/paper\_spine\_config.json\`
\- \`paper\_rewriting\_output/paper\_spine\_config.md\`

\## Config Fields

\| Field \| Allowed Values \| Default \|
\|---\|---\|---\|
\| \`workflow\` \| \`rewrite\_existing\`, \`build\_from\_materials\` \| — \|
\| \`scene\` \| \`journal\`, \`conference\`, \`report\_review\`, \`competition\` \| — \|
\| \`tier\` \| \`flash\`, \`pro\` \| \`flash\` \|
\| \`output\_language\` \| \`en\`, \`zh\` \| \`en\` for journal/conference; \`zh\` for Chinese requests \|
\| \`target\_name\` \| free text \| — \|
\| \`materials\_dir\` \| path or empty \| — \|
\| \`draft\_path\` \| path or empty \| — \|
\| \`user\_motivation\` \| free text or empty \| — \|
\| \`official\_urls\` \| list \| \`\[\]\` \|
\| \`special\_requirements\` \| list \| \`\[\]\` \|
\| \`word\_output\` \| \`none\`, \`docx\` \| \`docx\` \|
\| \`translation\_package\` \| \`none\`, \`zh\` \| \`none\` \|
\| \`reference\_mode\` \| \`local\_first\`, \`specified\_paths\`, \`web\` \| \`local\_first\` \|
\| \`reference\_paths\` \| list of local paths \| \`\["."\]\` \|
\| \`citation\_target\_count\` \| integer \| \`20\` \|
\| \`humanize\_tier\` \| \`none\`, \`light\`, \`medium\`, \`heavy\` \| \`medium\` \|

\## UI

\- The supported interactive path is the bundled terminal wizard (\`intake\_wizard.py\`).
\- In Claude Code, \`/paperspine\` launches the intake UI automatically when config is missing.
\- In Codex, use the absolute path to \`launch\_paperspine\_ui.ps1\` with escalated permissions.
\- Fallback: numbered menus; chat-based questions only when terminal execution is impossible.
\- Never require the user to hand-write JSON.

\## Scripts

\`\`\`bash
python scripts/intake\_wizard.py --output-dir paper\_rewriting\_output
\`\`\`