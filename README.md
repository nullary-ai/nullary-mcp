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

## Tools

The server exposes **35 tools** — served live via the MCP `tools/list` method. Full JSON
Schemas (inputs per tool) are in [`tools.json`](./tools.json). Tools span the seven
modalities plus cross-modality history, compound/provenance lookups, and the Layer-1
model registry.

| Tool | Description |
|---|---|
| `search_inactive_compounds` | Inactive small-molecule compound-target pairs. |
| `search_failed_selectivity` | Small molecules that failed selectivity. |
| `search_admet_failures` | Small-molecule ADMET failures. |
| `search_failed_guides` | Failed/ineffective CRISPR guides. |
| `search_failed_essentiality_screens` | Non-dependency / failed essentiality screens. |
| `search_ancestry_specific_failures` | Ancestry-specific CRISPR failures. |
| `search_developability_failures` | Antibody developability failures. |
| `search_failed_clinical_antibodies` | Discontinued/terminated clinical antibodies. |
| `search_failed_peptide_therapeutics` | Failed peptide therapeutics. |
| `search_peptide_stability_issues` | Peptide stability/half-life failures. |
| `search_failed_protacs` | PROTACs that failed degradation/ternary/permeability. |
| `search_protac_e3_issues` | PROTAC E3-ligase recruitment / ternary failures. |
| `search_failed_oligonucleotides` | ASOs/siRNAs that failed engagement/developability. |
| `search_oligo_delivery_failures` | Oligonucleotide delivery failures. |
| `search_failed_vaccines` | Failed/terminated vaccines (by pathogen/indication). |
| `search_vaccine_immunogenicity_failures` | Failed vaccine immunogen designs. |
| `search_failed_adcs` | ADCs that failed at any stage. |
| `search_adc_linker_failures` | ADC failures attributed to linker chemistry. |
| `search_failed_bispecifics` | Bispecifics that failed at any stage. |
| `search_bispecific_format_failures` | Bispecific format/engineering failures. |
| `search_admet_failures_all_modalities` | ADMET failures across ALL modalities. |
| `search_drug_drug_interaction_failures` | Drug-drug interaction failures. |
| `search_mechanism_failures` | Approaches that failed for a mechanism (by target). |
| `search_failed_replications` | Findings that failed to replicate. |
| `search_safety_failures` | Clinical/preclinical safety failures across modalities. |
| `search_target_history` | ALL failed approaches against a target across every modality. |
| `search_indication_history` | ALL failed approaches for an indication across every modality. |
| `search_pathogen_history` | Vaccine + antimicrobial + antibody failures for a pathogen. |
| `get_compound` | A compound + its full negative profile across modalities/sources. |
| `get_finding_provenance` | Full provenance + detail for a single finding by id. |
| `get_target_landscape` | Target "graveyard" / exhaustion index — how picked-over a target is, by modality and outcome. |
| `list_top_targets` | The most heavily-pursued targets, ranked by recorded negative findings. |
| `list_models` | Summary of the Layer-1 inactivity-scoring model registry. |
| `get_model_card` | Per-target Layer-1 model card: training counts + held-out scaffold-split metrics. |
| `get_coverage` | Per-modality and per-source coverage stats. |

## Links

- **Website:** https://nullary.ai
- **Docs:** https://nullary.ai/docs
- **Coverage:** https://nullary.ai/coverage
- **Research:** https://nullary.ai/research
- **MCP Registry:** listed as `ai.nullary/nullary`

## License

This documentation repository is MIT-licensed. The underlying data is provided under each
source's respective license — see the [coverage page](https://nullary.ai/coverage).
