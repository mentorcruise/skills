# MentorCruise Skills

Find mentors on [MentorCruise.com](https://mentorcruise.com) directly from Claude, Claude Code, Cursor, or any AI tool that supports skills. Search thousands of vetted mentors by skill, role, or expertise.

## Installation

Install via the [skills.sh](https://skills.sh) CLI:

```bash
npx skills add mentorcruise/skills
```

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

- Searches the MentorCruise mentor database via a REST API
- Clarifies ambiguous requests before searching (e.g., "PM" = Product or Project Management?)
- Enriches results with web research for deeper mentor profiles
- Presents up to 3 mentors with roles, fit explanations, and profile links
- Retries with alternative keywords when results are sparse
- Tracks shown mentors to avoid repeats when you ask for more

## How it works

The skill calls the MentorCruise search API to find mentors matching your request. No MCP servers, no API keys — just a simple REST endpoint. When you describe what you're looking for, it translates your request into optimized search queries with optional filters (location, language, skill, etc.), then enriches the top matches with web research to give you a personalized recommendation.

## Examples

**Specific request (searches immediately):**

```
> I'm building a marketplace app and need a mentor who's scaled a two-sided platform

**Marcus Chen** · VP of Product @ Deliveroo · 🇬🇧 United Kingdom
⭐ Top-rated mentor. Rated 4.9 stars (32 reviews).

Scaled a two-sided marketplace from early stage to IPO, so he's seen every
growth challenge you're about to face. His background in supply-demand
balancing and GTM strategy is a direct fit for what you're building.

👉 [View profile of Marcus](https://mentorcruise.com/mentor/...)
```

**Ambiguous request (clarifies first):**

```
> I need a PM mentor

Are you looking for Product Management or Project Management mentoring?
And what's your main goal — breaking into the field, leveling up, or interview prep?
```

**Career transition:**

```
> I want to move from backend to ML engineering

**Priya Sharma** · Senior ML Engineer @ Spotify · 🇸🇪 Sweden
Rated 5.0 stars (25 reviews).

She made the exact same transition from backend to ML three years ago and now
mentors engineers through it. Strong on Python, PyTorch, and system design for
ML pipelines — plus she can help you build a portfolio that stands out.

👉 [View profile of Priya](https://mentorcruise.com/mentor/...)
```

## License

MIT
