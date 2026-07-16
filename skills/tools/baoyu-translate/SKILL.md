\-\-\-
name: baoyu-translate
description: Translates articles and documents between languages with three modes - quick (direct), normal (analyze then translate), and refined (analyze, translate, review, polish). Supports custom glossaries and terminology consistency via EXTEND.md. Use when user asks to "translate", "翻译", "精翻", "translate article", "translate to Chinese/English", "改成中文", "改成英文", "convert to Chinese", "localize", "本地化", or needs any document translation. Also triggers for "refined translation", "精细翻译", "proofread translation", "快速翻译", "快翻", "这篇文章翻译一下", or when a URL or file is provided with translation intent.
version: 1.59.0
metadata:
 openclaw:
 homepage: https://github.com/JimLiu/baoyu-skills#baoyu-translate
 requires:
 anyBins:
 \- bun
 \- npx
\-\-\-

\# Translator

Three-mode translation skill: \*\*quick\*\* for direct translation, \*\*normal\*\* for analysis-informed translation, \*\*refined\*\* for full publication-quality workflow with review and polish.

\## Script Directory

Scripts in \`scripts/\` subdirectory. \`{baseDir}\` = this SKILL.md's directory path. Resolve \`${BUN\_X}\` runtime: if \`bun\` installed → \`bun\`; if \`npx\` available → \`npx -y bun\`; else suggest installing bun. Replace \`{baseDir}\` and \`${BUN\_X}\` with actual values.

\| Script \| Purpose \|
\|--------\|---------\|
\| \`scripts/main.ts\` \| CLI entry point. Default action splits markdown into chunks; also supports explicit \`chunk\` subcommand \|
\| \`scripts/chunk.ts\` \| Markdown chunking implementation used by \`main.ts\` and kept compatible for direct invocation \|

\## Preferences (EXTEND.md)

Check EXTEND.md existence (priority order):

\`\`\`bash
\# macOS, Linux, WSL, Git Bash
test -f .baoyu-skills/baoyu-translate/EXTEND.md && echo "project"
test -f "${XDG\_CONFIG\_HOME:-$HOME/.config}/baoyu-skills/baoyu-translate/EXTEND.md" && echo "xdg"
test -f "$HOME/.baoyu-skills/baoyu-translate/EXTEND.md" && echo "user"
\`\`\`

\`\`\`powershell
\# PowerShell (Windows)
if (Test-Path .baoyu-skills/baoyu-translate/EXTEND.md) { "project" }
$xdg = if ($env:XDG\_CONFIG\_HOME) { $env:XDG\_CONFIG\_HOME } else { "$HOME/.config" }
if (Test-Path "$xdg/baoyu-skills/baoyu-translate/EXTEND.md") { "xdg" }
if (Test-Path "$HOME/.baoyu-skills/baoyu-translate/EXTEND.md") { "user" }
\`\`\`

\| Path \| Location \|
\|------\|----------\|
\| \`.baoyu-skills/baoyu-translate/EXTEND.md\` \| Project directory \|
\| \`$HOME/.baoyu-skills/baoyu-translate/EXTEND.md\` \| User home \|

\| Result \| Action \|
\|--------\|--------\|
\| Found \| Read, parse, apply settings. On first use in session, briefly remind: "Using preferences from \[path\]. You can edit EXTEND.md to customize glossary, audience, etc." \|
\| Not found \| \*\*MUST\*\* run first-time setup (see below) — do NOT silently use defaults \|

\*\*EXTEND.md Supports\*\*: Default target language \| Default mode \| Target audience \| Custom glossaries (inline or file path) \| Translation style \| Chunk settings

Schema: \[references/config/extend-schema.md\](references/config/extend-schema.md)

\### First-Time Setup (BLOCKING)

\*\*CRITICAL\*\*: When EXTEND.md is not found, you \*\*MUST\*\* run the first-time setup before ANY translation. This is a \*\*BLOCKING\*\* operation.

Full reference: \[references/config/first-time-setup.md\](references/config/first-time-setup.md)

Use \`AskUserQuestion\` with all questions (target language, mode, audience, style, save location) in ONE call. After user answers, create EXTEND.md at the chosen location, confirm "Preferences saved to \[path\]", then continue.

\## Defaults

All configurable values in one place. EXTEND.md overrides these; CLI flags override EXTEND.md.

\| Setting \| Default \| EXTEND.md key \| CLI flag \| Description \|
\|---------\|---------\|---------------\|----------\|-------------\|
\| Target language \| \`zh-CN\` \| \`target\_language\` \| \`--to\` \| Translation target language \|
\| Mode \| \`normal\` \| \`default\_mode\` \| \`--mode\` \| Translation mode \|
\| Audience \| \`general\` \| \`audience\` \| \`--audience\` \| Target reader profile \|
\| Style \| \`storytelling\` \| \`style\` \| \`--style\` \| Translation style preference \|
\| Chunk threshold \| \`4000\` \| \`chunk\_threshold\` \| — \| Word count to trigger chunked translation \|
\| Chunk max words \| \`5000\` \| \`chunk\_max\_words\` \| — \| Max words per chunk \|

\## Modes

\| Mode \| Flag \| Steps \| When to Use \|
\|------\|------\|-------\|-------------\|
\| Quick \| \`--mode quick\` \| Translate \| Short texts, informal content, quick tasks \|
\| Normal \| \`--mode normal\` (default) \| Analyze → Translate \| Articles, blog posts, general content \|
\| Refined \| \`--mode refined\` \| Analyze → Translate → Review → Polish \| Publication-quality, important documents \|

\*\*Default mode\*\*: Normal (can be overridden in EXTEND.md \`default\_mode\` setting).

\*\*Style presets\*\* — control the voice and tone of the translation (independent of audience):

\| Value \| Description \| Effect \|
\|-------\|-------------\|--------\|
\| \`storytelling\` \| Engaging narrative flow (default) \| Draws readers in, smooth transitions, vivid phrasing \|
\| \`formal\` \| Professional, structured \| Neutral tone, clear organization, no colloquialisms \|
\| \`technical\` \| Precise, documentation-style \| Concise, terminology-heavy, minimal embellishment \|
\| \`literal\` \| Close to original structure \| Minimal restructuring, preserves source sentence patterns \|
\| \`academic\` \| Scholarly, rigorous \| Formal register, complex clauses OK, citation-aware \|
\| \`business\` \| Concise, results-focused \| Action-oriented, executive-friendly, bullet-point mindset \|
\| \`humorous\` \| Preserves and adapts humor \| Witty, playful, recreates comedic effect in target language \|
\| \`conversational\` \| Casual, spoken-like \| Friendly, approachable, as if explaining to a friend \|
\| \`elegant\` \| Literary, polished prose \| Aesthetically refined, rhythmic, carefully crafted word choices \|

Custom style descriptions are also accepted, e.g., \`--style "poetic and lyrical"\`.

\*\*Auto-detection\*\*:
\- "快翻", "quick", "直接翻译" → quick mode
\- "精翻", "refined", "publication quality", "proofread" → refined mode
\- Otherwise → default mode (normal)

\*\*Upgrade prompt\*\*: After normal mode completes, display:
\> Translation saved. To further review and polish, reply "继续润色" or "refine".

If user responds, continue with review → polish steps (same as refined mode Steps 4-6 in refined-workflow.md) on the existing output.

\## Usage

\`\`\`
/translate \[--mode quick\|normal\|refined\] \[--from \] \[--to \] \[--audience \] \[--style