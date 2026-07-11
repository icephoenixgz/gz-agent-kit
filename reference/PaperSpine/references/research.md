\# Research Stage

This file is the canonical stage playbook for the paper-spine orchestrator.

\## Purpose

Learn the target scene, index local references, study strong examples, map SOTA
gaps, and produce user-confirmable motivation options. Research must complete
before the user confirms the controlling motivation.

\## Literature Retrieval Priority Protocol

1\. \*\*Literature MCP tools (preferred).\*\* If the host has MCP servers matching
 \`cnki\`, \`ieee\`, \`arxiv\`, \`semantic scholar\`, \`scholar\`, \`pubmed\`, \`crossref\`,
 \`wos\`, \`web of science\`, or \`scopus\`, use them first. Record the source
 channel in \`source\_index.md\` as \`MCP-CNKI\`, \`MCP-IEEE\`, \`MCP-PubMed\`, etc.
2\. \*\*Host WebSearch / browsing tools (fallback).\*\*
3\. \*\*Local files (always available).\*\*
4\. \*\*local\_first rule:\*\* when \`reference\_mode=local\_first\` or \`specified\_paths\`,
 local index must be built first; MCP/web may supplement only.
5\. \*\*MCP is an enhancement, not a dependency.\*\* Do not error or ask the user to
 install MCP when none is available.

\## Tier Rules

\- \`flash\`: 3 target-scene examples + 3 recent high-quality field/SOTA examples.
\- \`pro\`: 6 target-scene examples + 6 recent high-quality field/SOTA examples.

\## Stage 1 — Index Local References

Create \`paper\_rewriting\_output/reference\_materials/source\_index.md\`:

\| Source ID \| Type \| Title/Name \| Origin/URL/Path \| Why Included \| Local File/Note \| Used For \|
\|---\|---\|---\|---\|---\|---\|---\|

Use \`scripts/reference\_inventory.py\`:
\`\`\`bash
python scripts/reference\_inventory.py . --output-dir paper\_rewriting\_output --mode local\_first
\`\`\`

\## Stage 2 — Three Parallel Specialist Sub-Agents

Launch all three simultaneously. Each agent gets only its own context.

\### Agent A: Scene Analyst → \`research\_dossier.md\`

Context: \`scene\`, \`target\_name\`, \`official\_urls\`, \`source\_index.md\`, scene reference file.

Sections: Venue Requirements, Review Criteria, Accepted Paper Patterns, Constraints for This Paper.

\### Agent B: Exemplar Learner → \`exemplar\_learning\_dossier.md\`

Context: \`tier\`, \`source\_index.md\`, scene reference path.

Sections: Exemplar Inventory table, Structural Patterns, Rhetorical Patterns, Language Patterns.

\### Agent C: SOTA Mapper → \`sota\_gap\_map.md\`

Context: \`tier\`, \`source\_index.md\`, \`user\_motivation\` (if set).

Table: Candidate Contribution \| What SOTA Already Does \| User Evidence \| Real Gap \| Claim Strength \| Risk. Plus Gap Summary.

\## Stage 3 — Merge

Produce \`style\_profile.md\` and \`motivation\_options\_after\_research.md\`. Stop for
user confirmation. Write \`confirmed\_motivation.md\` only after the user chooses,
revises, or writes their own motivation.

\## Required Outputs

\- \`reference\_materials/source\_index.md\`
\- \`research\_dossier.md\`
\- \`exemplar\_learning\_dossier.md\`
\- \`style\_profile.md\`
\- \`sota\_gap\_map.md\`
\- \`motivation\_options\_after\_research.md\`
\- \`confirmed\_motivation.md\` (after user confirmation)