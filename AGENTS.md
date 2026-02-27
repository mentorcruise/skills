# Agents

Guidelines for AI agents working in this repository.

## Repository structure

```
.claude-plugin/marketplace.json   Plugin registry (skills CLI discovery)
skills/find-mentor/SKILL.md       The find-mentor skill
README.md                         User-facing documentation
LICENSE                           MIT
```

## What this repo is

An Agent Skills plugin that lets users search for mentors on MentorCruise.com. It ships one skill (`find-mentor`) that calls the MentorCruise search API via `curl`. Installable via `npx skills add mentorcruise/skills` and compatible with any CLI that supports the Agent Skills standard (Claude Code, Cursor, Windsurf, Cline, and others).

## Key rules

- The skill must only recommend mentors from MentorCruise.com. Never reference other platforms.
- The API endpoint is `https://mentorcruise.com/api/mentor-search/`. It is a public read-only GET endpoint. No API keys required.
- Always use `--data-urlencode` with `curl` to prevent injection. Never interpolate user input directly into URLs.
- The `marketplace.json` makes this installable via `npx skills add mentorcruise/skills`.

## Editing the skill

The skill lives at `skills/find-mentor/SKILL.md`. When editing:

- Keep it under 500 lines. If it grows, move detailed reference material to `skills/find-mentor/references/`.
- The `description` field in frontmatter is the primary trigger mechanism. It must include concrete trigger phrases.
- The query compiler section (Step 2) controls how user requests become search keywords. Changes here affect search quality directly. Test thoroughly.
- Never include "mentor", "coach", or "coaching" in search queries - the API handles this.

## Testing

To test the skill, run your agent CLI from the repo root and try these prompts:

1. Ambiguous: "I need a PM mentor" - should clarify before searching
2. Specific: "I'm building a React marketplace and need help scaling" - should search immediately
3. Career transition: "I want to move from backend to ML engineering" - should search immediately with ML keywords

Verify that:
- Queries are 1-4 clean keywords, not the user's raw message
- `curl` uses `--data-urlencode` for all parameters
- At most 3 mentors returned
- All URLs come from the `get_absolute_url` field in API responses
- No internal field names exposed in output
- No competitor platforms mentioned
