# MentorCruise Skills

Find mentors on [MentorCruise.com](https://mentorcruise.com) directly from Claude, Claude Code, Cursor, or any AI tool that supports skills. Search thousands of vetted mentors by skill, role, or expertise.

## Installation

Install via the [skills.sh](https://skills.sh) CLI:

```bash
npx skills add mentorcruise/skills
```

This installs the skill and configures the MentorCruise search server automatically.

### Claude (web and desktop)

You can also use this skill in [Claude](https://claude.ai) directly:

1. Go to **Settings > Capabilities** and enable "Code execution and file creation"
2. Download this skill as a ZIP ([releases](https://github.com/mentorcruise/skills/releases) or zip the repo)
3. Go to **Customize > Skills**, click **+**, and select **Upload a skill**
4. Toggle the skill on

See [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude) for more details.

### Supported CLIs

This skill follows the open [Agent Skills](https://agentskills.io) standard and works with any compatible CLI, including:

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [Cursor](https://cursor.sh)
- [Windsurf](https://codeium.com/windsurf)
- [Cline](https://github.com/cline/cline)
- Any tool that supports the Agent Skills spec

## Skills

### find-mentor

Search for and recommend mentors from MentorCruise.com. Works with natural language. Describe what you need and get matched with up to 3 mentors.

**Invoke directly:**

```
/find-mentor product management for career transition
```

**Or let the agent detect it automatically:**

```
I need help transitioning from backend engineering to machine learning. Can you find me a mentor?
```

**What it does:**

- Searches the MentorCruise mentor database via Algolia
- Clarifies ambiguous requests before searching (e.g., "PM" = Product or Project Management?)
- Enriches results with web research for deeper mentor profiles
- Presents up to 3 mentors with roles, fit explanations, and profile links
- Retries with alternative keywords when results are sparse
- Tracks shown mentors to avoid repeats when you ask for more

## How it works

The skill connects to MentorCruise's Algolia-powered search index via an MCP server. When you describe what you're looking for, it translates your request into optimized search queries, filters results, and optionally enriches mentor profiles with web research to give you the best match.

## MCP Server

This plugin configures a remote MCP server for searching the MentorCruise mentor index. The server is read-only and requires no API keys. It uses a public search endpoint.

The configuration is in `.mcp.json`:

```json
{
  "mcpServers": {
    "mentorcruise": {
      "type": "url",
      "url": "https://mcp.eu.algolia.com/..."
    }
  }
}
```

## Examples

**Specific request (searches immediately):**

```
> I'm building a marketplace app and need a mentor who's scaled a two-sided platform

**Shammi Raichura** - Operations Lead at Uber
Scaled Uber's UK marketplace from day one with deep experience in GTM and
two-sided platform dynamics. Strong match if your challenge is growing supply
and demand simultaneously. Top-rated mentor. Rated 4.9 stars (32 reviews).

https://mentorcruise.com/mentor/shammiraichura/
```

**Ambiguous request (clarifies first):**

```
> I need a PM mentor

Are you looking for Product Management or Project Management mentoring?
And what's your main goal - breaking into the field, leveling up, or interview prep?
```

**Career transition:**

```
> I want to move from backend to ML engineering

**Chris Hammerschmidt** - Director of AI
Specializes in helping software engineers transition into ML, which is exactly
your situation. PhD in machine learning with 10+ years spanning research,
consulting, and engineering leadership. Top-rated mentor. Rated 5.0 stars
(25 reviews).

https://mentorcruise.com/mentor/chrishammerschmidt/
```

## License

MIT
