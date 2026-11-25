# UnHideA Research MCP Server

[![Official MCP Registry](https://img.shields.io/badge/MCP%20Registry-io.github.lijiumixin%2Funhidea--research--mcp-6366f1.svg)](https://registry.modelcontextprotocol.io/v0.1/servers/io.github.lijiumixin%2Funhidea-research-mcp/versions/latest)
[![UnHideA Wall Street Research MCP connector](https://glama.ai/mcp/connectors/io.github.lijiumixin/unhidea-research-mcp/badges/score.svg)](https://glama.ai/mcp/connectors/io.github.lijiumixin/unhidea-research-mcp)
[![MCP](https://img.shields.io/badge/MCP-Streamable%20HTTP-111827.svg)](https://unhidea.com/en/mcp)
[![Auth](https://img.shields.io/badge/Auth-OAuth%202.0%20%2B%20Bearer-2563eb.svg)](https://unhidea.com/en/mcp)
[![Tools](https://img.shields.io/badge/Tools-14-16a34a.svg)](#available-tools)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Remote Streamable HTTP & OAuth 2.0 Model Context Protocol (MCP) server for Wall Street sell-side equity research, cross-institution company packs, sourced rating/target-price histories, and point-in-time research replay.**

- **Official MCP Registry ID:** `io.github.lijiumixin/unhidea-research-mcp` (`v1.0.0`)
- **Remote Endpoint:** `https://mcp.unhidea.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** OAuth 2.0 Dynamic Client Registration (`research:read`, `research:write`) or personal Bearer key (`Authorization: Bearer <key>`)
- **Documentation & Key Setup:** https://unhidea.com/en/mcp (中文说明：https://unhidea.com/zh-hans/mcp)
- **Live Company & Bank Hubs:** [Companies](https://unhidea.com/en/companies) · [Institutions](https://unhidea.com/en/institutions) · [Research Library](https://unhidea.com/en/library)
- **Companion Open Dataset (MIT):** [wall-street-research-entities](https://github.com/lijiumixin/wall-street-research-entities) (405 global companies + 73 sell-side institutions across 11 languages)
- **Updates on X:** https://x.com/UnHideA

---

## Why UnHideA Research MCP?

Most financial MCP servers only expose raw price quotes or SEC filings. **UnHideA Research MCP** focuses on **institutional sell-side equity research** (Goldman Sachs, Morgan Stanley, J.P. Morgan, Citi, Bank of America, Bernstein, Evercore ISI, HSBC, Nomura, Barclays, Deutsche Bank, and more) with strict grounding and point-in-time hygiene:

- **Cross-bank comparison packs** (`research_pack`) to see where Wall Street desks agree or split on one company
- **Sourced ratings, price targets, and forecast verification** (`research_metric_history`, `research_forecast_outcomes`) matched by period, currency, unit, and basis
- **Counter-evidence retrieval** (`evidence_candidates`) to pull verbatim quotes supporting *or challenging* an investment thesis
- **Point-in-time snapshots** (`replay_research`) accumulated since initial indexing for clean historical replay without look-ahead bias
- **Deduplicated bilingual coverage** across Chinese originals and verified English translations, with direct links to full web briefs and authenticated on-site PDF readers

---

## Quick Start

### Option 1: OAuth 2.0 (Clients Supporting Dynamic Client Registration)

Add the remote server URL directly in your MCP client (e.g., Claude, ChatGPT, or OAuth-capable MCP hosts):

```text
https://mcp.unhidea.com/mcp
```

OAuth metadata discovery is served automatically at:
`https://mcp.unhidea.com/.well-known/oauth-protected-resource`

Supported scopes:
- `research:read` — search, fetch, packs, clusters, evidence, metric history, replay, and read watchlist
- `research:write` — update persistent watchlist and submit topic requests

### Option 2: Bearer Key (Cursor, Antigravity, Windsurf, Custom Agents)

1. Sign in and generate a personal MCP key at https://unhidea.com/en/mcp (or https://unhidea.com/zh-hans/mcp).
2. Add the server to your `mcp_config.json` / `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "unhidea-research": {
      "url": "https://mcp.unhidea.com/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_UNHIDEA_MCP_KEY>"
      }
    }
  }
}
```

---

## Available Tools (14)

| Tool | Purpose |
| --- | --- |
| `search` | Find published UnHideA research by title, institution, ticker, topic, keyword, or date (deduplicated per original report, with on-site PDF reader links where archived). |
| `fetch` | Retrieve the public synopsis, verbatim section excerpts, and archived PDF reader URL for a research ID. |
| `research_pack` | Pull latest coverage on a tagged company, cross-institution views, and prior reports from the latest covering desk. |
| `research_updates` | Track new research across multiple tickers or topics over a rolling window (default 7 days). |
| `coverage_map` | Map a topic or filtered query by co-occurring themes, covered companies, institutions, cited examples, and a reading shortlist. |
| `event_clusters` | Identify shared-event coverage where multiple banks published on the same company/catalyst on the same report date. |
| `evidence_candidates` | Retrieve verbatim public excerpts matching a claim—with optional `counter_query` to surface challenging evidence. |
| `research_metric_history` | Return sourced ratings, price targets, and financial forecasts over time with period, currency, unit, and basis metadata. |
| `research_forecast_outcomes` | Match historical forecast claims against subsequent reported disclosures (flagging unverified items honestly). |
| `replay_research` | Query point-in-time historical index snapshots accumulated since initial publication. |
| `get_watchlist` | Read your saved companies and research topics watchlist. |
| `set_watchlist` | Save or update your tracked companies and research topics (`research:write`). |
| `watchlist_updates` | Poll recent research updates for every company and topic on your watchlist. |
| `submit_topic_request` | Submit a new company, sector, or theme coverage request (`research:write`). |

---

## Example Prompts

- *"Use `research_pack` for Microsoft and summarize where Goldman Sachs, HSBC, Citi, Nomura, and Bank of America disagree on FY27 Azure growth vs. capex."*
- *"Run `evidence_candidates` on Apple with `query: gross margin memory costs` and `counter_query: App Store revenue acceleration`."*
- *"Check `research_metric_history` for Meta over the last quarter and list every sourced price target change."*
- *"Use `event_clusters` to find all multi-bank reactions published this week on semiconductor earnings."*

---

## Support & License

- Website: https://unhidea.com/en/
- Support: help@unhidea.com
- X: https://x.com/UnHideA
- Documentation & manifest license: [MIT](LICENSE)
