# Agents

Guidelines for AI agents working in this repository.

## Repository structure

```
.claude-plugin/marketplace.json   Plugin registry (skills CLI discovery)
.mcp.json                         MentorCruise Algolia MCP server config
skills/find-mentor/SKILL.md       The find-mentor skill
README.md                         User-facing documentation
LICENSE                           MIT
```

## What this repo is

An Agent Skills plugin that lets users search for mentors on MentorCruise.com. It ships one skill (`find-mentor`) backed by an Algolia MCP server for real-time mentor search. Installable via `npx skills add mentorcruise/skills` and compatible with any CLI that supports the Agent Skills standard (Claude Code, Cursor, Windsurf, Cline, and others).

## Key rules

- The skill must only recommend mentors from MentorCruise.com. Never reference other platforms.
- The `.mcp.json` configures a read-only public Algolia search endpoint. No API keys required.
- The `marketplace.json` makes this installable via `npx skills add mentorcruise/skills`.

## Editing the skill

The skill lives at `skills/find-mentor/SKILL.md`. When editing:

- Keep it under 500 lines. Currently ~200 lines. If it grows, move detailed reference material to `skills/find-mentor/references/`.
- The `description` field in frontmatter is the primary trigger mechanism. It must include concrete trigger phrases.
- The search compiler section (Step 2) contains the exact Algolia tool call format. Changes here affect search quality directly. Test thoroughly.
- `facet_filters` must always be `List[List[str]]` (nested lists). This is the most common source of tool call errors.
- Base filters (`saved_open_spots > 0 AND saved_recommendation_value >= 100`) are always enforced. Do not remove them.

## Testing

To test the skill, run your agent CLI from the repo root and try these prompts:

1. Ambiguous: "I need a PM mentor" - should clarify before searching
2. Specific: "I'm building a React marketplace and need help scaling" - should search immediately
3. Career transition: "I want to move from backend to ML engineering" - should search immediately with ML keywords

Verify that:
- Queries are 1-4 clean keywords, not the user's raw message
- `facet_filters` are nested lists, never flat
- At most 3 mentors returned
- All URLs are `https://mentorcruise.com/...`
- No internal field names exposed in output
- No competitor platforms mentioned
