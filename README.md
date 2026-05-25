# Nullary MCP Server

**Negative results intelligence for drug discovery — over the [Model Context Protocol](https://modelcontextprotocol.io).**

Nullary is a hosted MCP server that lets AI agents query **measured negative results** from
drug discovery: inactive compounds, failed selectivity panels, terminated clinical trials,
failed CRISPR screens, antibody developability failures, and more — each result carrying full
provenance (source database, DOI/PMID, license).

This repository documents the **public MCP interface**. The server is hosted; the data
pipeline and application code are maintained separately.

## Connect

Nullary is a **remote** MCP server (streamable-HTTP) — nothing to install, no API key:

```
https://mcp.nullary.ai/mcp
```

### Claude Code / generic MCP client

```json
{
  "mcpServers": {
    "nullary": {
      "url": "https://mcp.nullary.ai/mcp"
    }
  }
}
```

### Cursor

Settings → **MCP** → *Add new MCP server* → paste the URL above (transport: streamable-HTTP).

### Claude Desktop

Settings → **Connectors** → *Add custom connector* → URL `https://mcp.nullary.ai/mcp`.

## What you can ask

- *"What's failed against EGFR?"* — failed compounds, trials, and screens for a target, across modalities
- *"Which kinase inhibitors were inactive in ChEMBL?"*
- *"Show terminated Phase 2 oncology trials and why they stopped"*
- *"Failed CRISPR knockouts for TP53"*

Tools are organized by modality (small molecule, CRISPR, antibody, peptide, PROTAC, clinical
trial, …); every response cites its source.

## Links

- **Website:** https://nullary.ai
- **Docs:** https://nullary.ai/docs
- **Coverage:** https://nullary.ai/coverage
- **Research:** https://nullary.ai/research
- **MCP Registry:** listed as `ai.nullary/nullary`

## License

This documentation repository is MIT-licensed. The underlying data is provided under each
source's respective license — see the [coverage page](https://nullary.ai/coverage).
