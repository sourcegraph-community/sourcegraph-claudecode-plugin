# sourcegraph-claudecode-plugin

Sourcegraph plugin for Claude Code that adds:

- Sourcegraph MCP server connectivity (code search, navigation, Deep Search)
- `/sourcegraph:sg-search` and `/sourcegraph:sg-file` skills
- `searching-sourcegraph` agent skill for disciplined search workflows

## Prerequisites

- [Claude Code](https://code.claude.com) version 1.0.33 or later (`claude --version`)
- A Sourcegraph instance with MCP enabled
- A Sourcegraph access token with `mcp` scope

Set the required environment variables in your shell profile (`.zshrc`, `.bashrc`, etc.):

```bash
export SOURCEGRAPH_ENDPOINT="https://sourcegraph.example.com"
export SOURCEGRAPH_ACCESS_TOKEN="<your-token>"
```

## Install (permanent)

Add this repository as a marketplace, then install the plugin:

```bash
# From a local clone
claude plugin marketplace add ./sourcegraph-claudecode-plugin

# Or directly from GitHub
claude plugin marketplace add sourcegraph-community/sourcegraph-claudecode-plugin
```

Then install:

```bash
claude plugin install sourcegraph@sourcegraph-claudecode-plugin
```

Restart Claude Code after installing.

## Install (per-session, for development)

Load the plugin for a single session without installing permanently:

```bash
claude --plugin-dir ./sourcegraph-claudecode-plugin
```

Run `/reload-plugins` after making changes during a session.

## Alternative: add MCP server only

If you only want the Sourcegraph MCP tools without the skills, add the server directly:

```bash
claude mcp add --transport http sourcegraph \
  "${SOURCEGRAPH_ENDPOINT}/.api/mcp" \
  --header "Authorization: token ${SOURCEGRAPH_ACCESS_TOKEN}"
```

## Verify

After installing, confirm everything loaded:

- `/help` should list `sourcegraph:sg-search`, `sourcegraph:sg-file`, and `sourcegraph:searching-sourcegraph`
- `/mcp` should show the `sourcegraph` MCP server as connected

## Structure

```text
.
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── .mcp.json
├── skills/
│   ├── sg-search/
│   │   └── SKILL.md
│   ├── sg-file/
│   │   └── SKILL.md
│   └── searching-sourcegraph/
│       └── SKILL.md
└── README.md
```

## Skills

| Skill | Invocation | Purpose |
|-------|------------|---------|
| `sg-search` | `/sourcegraph:sg-search <query>` | Search Sourcegraph with natural language or keyword syntax |
| `sg-file` | `/sourcegraph:sg-file <repo> [rev] <path>` | Fetch and summarize a file from Sourcegraph |
| `searching-sourcegraph` | Auto-invoked by Claude | Disciplined search and navigation workflow using all Sourcegraph MCP tools |

## MCP Details

- Endpoint: `${SOURCEGRAPH_ENDPOINT}/.api/mcp`
- Transport: HTTP (`"type": "http"`)
- Auth header: `Authorization: token <token>`

## Built from

- [sourcegraph-cursor-plugin](https://github.com/sourcegraph-community/sourcegraph-cursor-plugin)
- [sourcegraph-gemini](https://github.com/sourcegraph-community/sourcegraph-gemini)
- [sourcegraph-skill](https://github.com/sourcegraph-community/sourcegraph-skill)

## Docs

- [Claude Code plugins](https://code.claude.com/docs/en/plugins)
- [Sourcegraph MCP](https://sourcegraph.com/docs/api/mcp)
