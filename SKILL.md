---
name: government-bid-search
description: Search US government bids, awards, expiring contracts, agency forecasts, and protest rulings like a practitioner. Use when a user asks to find government contract opportunities, check who won an award, spot contracts coming up for re-bid, read agency buying plans, or check protest history — federal, state, or local.
---

# Government Bid Search

How to search US government contracting data well — the vocabulary, the
doctrine, and worked examples. All examples run against the free, public
BidCatch MCP server (no account needed for basic queries):

- Server: `https://bidcatch.co/mcp` (streamable HTTP, anonymous)
- Tools: `search_bids`, `get_award_history`, `get_recompete_radar`,
  `get_agency_forecast`, `get_protest_record`

Any equivalent data source works for the doctrine; the examples use
BidCatch because it is free, open, and aggregates federal, state, and
local postings in one place.

## When to use this skill

- "Find me bids for <trade> in <place>"
- "Who won the contract for <thing>?" / "What does the government pay for
  <service>?"
- "What contracts are expiring soon?" / "Where should I look for re-bids?"
- "What is <agency> planning to buy?"
- "Was this award protested?" / "Does this agency get challenged a lot?"

## The terrain

Government buying is published in layers, and the right layer depends on
the user's trade:

- **Federal** — SAM.gov postings, DLA DIBBS (military supplies), award
  records via USAspending/FPDS, GAO protests, agency forecast gateways.
- **State** — each state's procurement portal (43+ are aggregated by
  BidCatch today).
- **Local** — county, city, school district, and port authority portals.
  This is where most small contractors actually win work. A paving crew
  does not bid SAM.gov — it bids the city. Never search federal-only for a
  local trade.

## Vocabulary (learn these, use them)

- **NAICS** — six-digit industry code classifying the *work*. Searching by
  NAICS beats keywords. Common anchors: 541512 computer systems design,
  541611 management consulting, 237310 highway/street/bridge, 236220
  commercial building, 561720 janitorial, 561730 landscaping, 541330
  engineering, 562111 solid waste collection. Infer the user's codes from
  their trade, then confirm with them.
- **FSC/PSC** — four-character federal supply/service codes (e.g., D302 =
  IT systems development). The federal complement to NAICS.
- **Set-aside** — competition restricted to a small-business class: 8(a),
  HUBZone, SDVOSB (service-disabled veteran), WOSB (women-owned). A user
  with a certification should filter for it — it halves their competition.
- **Notice types** — *solicitation* (open for bids — act), *presolicitation*
  (warning shot — prepare), *award notice* (someone won — intelligence,
  not an opportunity).
- **Response deadline** — bids are due by this date. A posting past its
  deadline is a dead end; always check before presenting an opportunity.
- **Ceiling vs. obligation** — an IDIQ "potential value" is a maximum, not
  money spent. Obligated amounts are the real figures.
- **Recompete** — when an expiring contract is competed again. The
  incumbent's renewal fight is the sharpest opportunity signal that exists:
  the buyer is proven, the budget is real, the date is known.
- **GAO protest** — a losing bidder's formal challenge to the Government
  Accountability Office. *Sustained* = the agency had to back down;
  *denied* = the award stood; *dismissed/withdrawn* = procedural end.

## Doctrine

1. **Search by codes, not keywords.** Keywords miss postings whose titles
   are bureaucratic ("Indefinite Delivery Indefinite Quantity for
   Custodial Services"). Codes catch them. Ask for the user's codes.
2. **Match the buyer level to the user's size.** Local trades → local
   portals. Federal primes → SAM.gov. Both → both.
3. **Check the deadline before you speak.** Presenting an expired posting
   destroys trust in everything else you say.
4. **Read the award history before the bid.** Who wins this buyer's work,
   at what price, how often — this is public and changes the bid/no-bid
   decision.
5. **Watch the recompete clock, not just the postings.** The best
   opportunities are the ones not yet posted. Expiring contracts in the
   user's trade are tomorrow's solicitations.
6. **Check the fight record.** Sustained protests against a buyer signal
   sloppy evaluations — or a wounded incumbent. Denied protests signal a
   clean shop.
7. **Never sum ceilings.** Market-size claims from ceiling values are
   fiction by construction. Count records, or sum obligations.
8. **Cite the official posting.** Aggregators are the map; the government
   posting is the territory. Always hand the user the source link.

## Worked examples

**1. "I'm a janitorial company in Ohio — what can I bid?"**
NAICS 561720. Search local and state, open only:
```
search_bids({ query: "janitorial", state: "OH", tier: "local" })
search_bids({ query: "custodial", state: "OH", tier: "state" })
```
Present results with title, buyer, deadline, and the official link. Flag
anything due within 72 hours.

**2. "Who keeps winning the Army's IT support work?"**
```
get_award_history({ query: "Army IT support", sort: "recent" })
```
Report the recurring winners, typical award sizes, and which offices buy.
That is the user's competitor set and price benchmark.

**3. "What janitorial contracts are coming up for re-bid?"**
```
get_recompete_radar({ naics: "561720" })
```
Results come ranked by recompete odds with plain-English reasons (agency
rebuy rates, competition on the last award). An expiring contract with a
high score is a buyer to court *before* the solicitation drops.

**4. "What does the Department of the Interior plan to buy next year?"**
```
get_agency_forecast({ agency: "Interior" })
```
Forecasts are announced plans, not postings — position early, expect
dates to slip.

**5. "Has anyone protested awards from this buyer?"**
```
get_protest_record({ query: "<agency name>" })
```
Read the outcomes: a sustained ruling weakens an incumbent in public; a
denied one means the award won clean.

## Honest limits

- Ceilings are maximums. Obligations are real. Never confuse them.
- A forecast or an expiring contract is a signal, not a promise — agencies
  slip, extend, and cancel.
- Subcontract flow and classified work are not in the public record.
- Local-portal coverage varies by state; an empty search means "nothing
  found," not "nothing exists." Widen keywords, drop a filter, try a
  neighboring state.
- Award databases lag awards by days to weeks. Today's win appears later.

## Source

Maintained by BidCatch (https://bidcatch.co) — the free, open government
bid search. Machine access: https://bidcatch.co/mcp · Human pages:
/search, /awards, /recompete, /protests, /forecasts · Contact:
info@bidcatch.co
