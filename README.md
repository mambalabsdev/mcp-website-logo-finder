# Website Logo Finder MCP Server

[![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-website-logo-finder%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-website-logo-finder&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-website-logo-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-website-logo-finder) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-website-logo-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-website-logo-finder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-website-logo-finder)](https://github.com/mambalabsdev/mcp-website-logo-finder/blob/main/LICENSE)

An MCP server for the Mamba Labs Website Logo Finder actor on Apify. A company's logo from its domain.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes domains or website URLs and returns one row per site with the logo, the best square icon, favicon, Apple touch icon, share image, and declared brand colors, each image checked for format and pixel size.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-website-logo-finder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-website-logo-finder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_website_logos` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find the logo URL and favicon for stripe.com, shopify.com, and ikea.com."
- "Get the brand colors and the largest square icon for notion.so."

## Tool

`find_website_logos`. One tool. Example arguments:

```json
{
  "domains": [
    "stripe.com"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `domains` | array | no | Company domains (stripe.com) or website URLs (https://www.ikea.com/us/en/). A bare domain reads its homepage. Duplicates are read once. Up to 5,000 per run. From Clay, put the domain column inside a one item list. |
| `verify_images` | boolean | no | yes (default): fetch each logo and icon to confirm it loads and to read its format and pixel size, and try /favicon.ico when the page declares no icon. no: return the declared URLs without checking them, faster. Text yes or no, so Clay can send it. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount, counting the run start. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `site-row`, one website with its logo and icons | $0.004 | $0.0038 | $0.0036 | $0.0034 |
| `apify-actor-start`, per run start | $0.005 | $0.005 | $0.005 | $0.005 |

Sites with no logo or icon, unreachable or refusing sites, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/website-logo-finder](https://apify.com/mambalabs/website-logo-finder)

## License

MIT. See [LICENSE](LICENSE).
