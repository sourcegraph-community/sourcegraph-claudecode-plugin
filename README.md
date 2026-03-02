# sourcegraph-claudecode-plugin

Sourcegraph plugin for Claude Code that adds:

- Sourcegraph MCP server connectivity
- Reusable Sourcegraph commands
- A `searching-sourcegraph` skill for agent workflows

Built from:

- https://github.com/sourcegraph-community/sourcegraph-cursor-plugin
- https://github.com/sourcegraph-community/sourcegraph-gemini
- https://github.com/sourcegraph-community/sourcegraph-skill

and aligned with:

- Claude Code plugin docs: https://code.claude.com/docs/en/plugins
- Sourcegraph MCP docs: https://sourcegraph.com/docs/api/mcp

## Structure

```text
.
├── .claude-plugin/
│   └── plugin.json
├── .mcp.json
├── commands/
│   ├── sg-file.md
│   └── sg-search.md
├── skills/
│   └── searching-sourcegraph/
│       └── SKILL.md
└── README.md
```

## Use In Claude Code

Run Claude Code with this plugin directory:

```bash
claude --plugin-dir ./sourcegraph-claudecode-plugin
```

Or from this repository root:

```bash
claude --plugin-dir .
```

Then restart Claude Code after changes and verify:

- `/help` shows `/sourcegraph:sg-search` and `/sourcegraph:sg-file`
- `/mcp` shows the `sourcegraph` MCP server

## Configuration

Set environment variables used by `.mcp.json`:

- `SOURCEGRAPH_ENDPOINT` (for example `https://sourcegraph.com`)
- `SOURCEGRAPH_ACCESS_TOKEN` (personal access token with `mcp` scope)

Example:

```bash
export SOURCEGRAPH_ENDPOINT="https://sourcegraph.example.com"
export SOURCEGRAPH_ACCESS_TOKEN="<your-token>"
```

## Verified MCP Details

This plugin follows Sourcegraph MCP docs:

- Endpoint is `${SOURCEGRAPH_ENDPOINT}/.api/mcp`
- HTTP transport is used (`"type": "http"`)
- Access token auth header is `Authorization: token <token>`

Also compatible with OAuth-first setup from docs:

```bash
claude mcp add --transport http sg https://sourcegraph.example.com/.api/mcp
```

## Included Commands

- `/sourcegraph:sg-search` to run Sourcegraph search workflows
- `/sourcegraph:sg-file` to fetch a file and summarize it

## Included Skill

- `searching-sourcegraph` for disciplined Sourcegraph search and navigation workflows
