# Government Bid Search — agent skill

A [Claude skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
(and portable markdown guide) that teaches AI agents how to search US
government bids and contracts like a practitioner: the vocabulary (NAICS,
FSC/PSC, set-asides, notice types), the doctrine (search by codes not
keywords, match the buyer level, check deadlines, read award history,
watch the recompete clock), and worked examples.

The examples run against the free public BidCatch MCP server
(`https://bidcatch.co/mcp`, anonymous, no account) — the doctrine works
with any data source.

## Use it

- **Claude (skills):** copy `SKILL.md` into your skills directory, or point
  your agent config at this repo.
- **Any agent:** paste `SKILL.md` into the system/context, or connect to
  the BidCatch MCP server — its `instructions` block carries the same
  doctrine and arrives automatically on connect.

## What it covers

- Finding open bids for a trade + place (federal, state, local)
- Researching who wins what, and for how much
- Spotting expiring contracts before they are re-bid
- Reading agency procurement forecasts
- Checking GAO protest history
- The honest limits of public procurement data (ceilings ≠ spending)

## Links

- BidCatch: https://bidcatch.co
- MCP server: https://bidcatch.co/mcp
- Machine-access details: https://bidcatch.co/partners
