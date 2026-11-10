# How to connect Partiful to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Partiful account.** Partiful has no official app in the ChatGPT or Claude directories. Cotlet.dev connects your own signed-in Partiful account to any AI agent, so you can ask in plain words and the AI creates events, invites guests and tracks RSVPs for you.

## What you can ask

> Create a "Spring Open House" event for Saturday, April 18 at 6 pm at 42 Main Street and invite my 30 regular customers.

> Who hasn't replied to the Friday wine tasting yet? List their names.

> Send a reminder to everyone who said yes to Thursday's workshop: doors open at 5:30 pm.

> How many guests are going, maybe and not going for the June 12 launch party?

> Invite Maria Lopez, Tom Becker and Priya Shah to next Sunday's brunch and tell them to bring a plus one.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Partiful tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"partiful":{"command":"uvx","args":["partiful-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t partiful-mcp .
docker run -i --rm -e COTLET_API_KEY partiful-mcp
```

Tools: `partiful_guide`, `partiful_status`, `partiful_open`, `partiful_read`, `partiful_click`, `partiful_type`, `partiful_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install partiful-mcp        # or run it once: uvx partiful-mcp connect
partiful-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 partiful_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 partiful_agent.py status    # is Partiful ready in your Cotlet.dev account
python3 partiful_agent.py guide     # Partiful screens and sign-in link
python3 partiful_agent.py read      # open Partiful, read the page, close the browser
python3 partiful_agent.py tools     # list Cotlet.dev tools
python3 partiful_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Partiful users

**Does Partiful have an API?**

Partiful has no official app or connector in ChatGPT or Claude. Cotlet.dev works in your own signed-in Partiful account, so your AI agent can create events, invite guests and track RSVPs without a Partiful API key.

**How do I connect Partiful to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Partiful once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Partiful API key.

**Is there a way to use Claude with Partiful?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Partiful account.

**Is there a Partiful MCP server?**

Partiful has no official connector in the ChatGPT or Claude directories. Cotlet.dev is a hosted MCP server that works in Partiful for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Partiful on Cotlet.dev](https://cotlet.dev/integrations/partiful-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=partiful&utm_content=find)
- [PyPI package partiful-mcp](https://pypi.org/project/partiful-mcp/)
- [Odel](https://odel.app/modules/cotlet/partiful)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-partiful-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/partiful-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=partiful

Start free: https://cotlet.dev/signup?app=partiful&utm_source=github&utm_medium=readme&utm_campaign=partiful
