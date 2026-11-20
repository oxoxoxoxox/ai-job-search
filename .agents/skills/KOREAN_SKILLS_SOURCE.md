# Korean Skills installation source

- Upstream: https://github.com/DaleSeo/korean-skills
- Commit: ae12ba27982ebeff03b46dc738365aaa34260d9a
- Source: https://github.com/DaleSeo/korean-skills/tree/ae12ba27982ebeff03b46dc738365aaa34260d9a
- Installed: 2026-11-20 (Asia/Seoul)
- Scope: this repository's `.agents/skills/`; no global installation.
- Method: Codex skill-installer helper, pinned GitHub commit.

| Installed folder | Upstream path | SKILL.md version |
|---|---|---|
| humanizer | skills/humanizer | 1.6.0 |
| grammar-checker | skills/grammar-checker | 1.0.1 |
| style-guide | skills/style-guide | 1.1.0 |

Original SKILL.md files, references, and examples are included, with the single path correction below. The original upstream MIT LICENSE is included in each installed skill folder so copies of an individual skill retain the notice. Local patch: in humanizer/references/structure-patterns.md, corrected ../../../style-guide/references/tone-consistency.md to ../../style-guide/references/tone-consistency.md so the sibling-skill link resolves. No prose or other upstream content is modified.

Project-specific guidance lives outside these upstream folders. Claude-style tool names in the source are mapped to available Codex operations; they do not grant permissions. No Claude plugin or remote MCP was installed.

To update: review upstream changes, select a commit, replace each complete skill folder while preserving the license, update this record, and check discovery metadata, reference links, and factual-preservation behavior. Avoid a second competing copy in a user-global skill directory.
