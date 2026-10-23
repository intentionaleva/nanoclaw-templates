# Wren: household emergency-preparedness companion

A NanoClaw agent template for private households. Wren asks about ten questions, looks up the hazards that are real for where you live, work and travel (and shows you the source), and builds one plan sized to your people, your needs and your budget. The plan is tiered: red for this week, amber for the next couple of months, green for the bigger upgrades over the year. Then Wren checks in once a week until it's done, reviews the kit monthly for expiries, and re-runs the risks every quarter.

It works from official civil-protection guidance: ready.gov (FEMA) and the German BBK brochure "Vorsorgen für Krisen und Katastrophen" (11/2025) are built in; for other countries it finds the national equivalent. No survivalist content, no weapons, no doom. The pitch is the BBK's own: every bit of preparation counts, and three days of water already changes a lot.

Author: Eva.

## Layout

```
wren/
├── plugin.json
├── mcp.json                                # optional: osm-mcp (OpenStreetMap), no key
├── ai.nanoco.nanoclaw/
│   ├── context/
│   │   ├── instructions.md                 # persona and ground rules
│   │   └── additional_context/
│   │       ├── plan-format.md              # exact shape of the prep/ files
│   │       └── sources.md                  # which official bodies to use, per country
│   └── tasks/                              # created PAUSED
│       ├── weekly-check-in.md
│       ├── monthly-kit-review.md
│       └── quarterly-plan-review.md
├── skills/
│   ├── welcome/SKILL.md                    # first contact, runs onboarding
│   └── wren/
│       ├── SKILL.md                        # router
│       └── references/
│           ├── onboarding.md               # 10 questions in 5 blocks
│           ├── risk-assessment.md          # hazard lookup per location, with sources
│           ├── plan-builder.md             # red/amber/green rules, sizing, timeline
│           ├── budget-tiers.md             # what €0 / €50 / €500 / €5k buy
│           ├── checklists.md               # BBK and ready.gov lists, sized per household
│           ├── communication-plan.md       # the family emergency card
│           ├── special-needs.md            # children, seniors, disability, pets
│           ├── check-ins.md                # weekly, monthly, quarterly mechanics
│           ├── drills-and-alerts.md        # siren meanings, shelter rules, drills
│           ├── safety.md                   # scope and refusals
│           └── nearby.md                   # places and foot routes via the osm server
└── README.md
```

Hazard maps, alert apps and official pages come from the runtime's web search. The one declared server, `osm`, is optional and keyless (see Services below); without it Wren still runs end to end and just skips the place lookups.

## What it does

| Step | What happens |
|------|--------------|
| Onboarding | People and age bands, pets, home and regular locations, trips, medical and access needs, goal (3 / 10 / 30+ days), budget, what's already in place, check-in day. One block per message. |
| Risk assessment | Flood zone, storm, heat, winter, power-cut exposure, water supply, wildfire, earthquake, industrial and nuclear sites in range, the official alert app and sirens. Every hazard carries its source and the date checked. Trips get a lighter pass and a travel card. |
| Plan | Red: this week, €0, under an hour each (alert app, communication card, 3 days of water, medication reserve requested, documents photographed). Amber: 4 to 8 weeks, the stock and the kits, spread so no week exceeds the budget. Green: 3 to 12 months, power, heating, comms, training, structural. Quantities are computed and shown. |
| Communication card | ready.gov's structure: out-of-area contact, three meeting places, schools with pickup policy, numbers. One printed page per person. With the `osm` server the meeting places are real candidates with foot times from home and school. |
| Nearby help (optional) | Nearest pharmacy, hospital, fire station, shelter with foot distance, from OpenStreetMap; re-checked quarterly. Never used for hazard likelihood. |
| Check-ins | Weekly: three items, one question, no repeated nags. Monthly: expiries and rotation. Quarterly: risks re-run, season check, household changes, one drill. |

State lives in the agent's workspace under `prep/`: `profile.md`, `risks.md`, `plan.md`, `comms-card.md`, `log.md`.

## What it deliberately doesn't do

Weapons or "home defence". Bunkers and wilderness survival. Medical advice beyond official first aid and "call the emergency number". Medication stockpiling beyond a doctor-agreed reserve. Fuel or heating advice that contradicts the manufacturer or the indoor-use rule. Geopolitical commentary. Business continuity. If someone describes an emergency in progress, Wren gives the emergency number and the one official instruction and stops planning.

## Configure before first use

Nothing. First contact runs the onboarding. If the household lives outside Germany or the US, Wren searches for the national civil-protection guidance and says what it found.

## Stamp an agent

```bash
ncl groups create --template lifestyle/wren --name "Wren"
```

Wire it to the household's chat with `/manage-channels`. A family group chat works well; Wren addresses the whole household.

## Recurring tasks

All three ship paused. At the end of onboarding Wren confirms the check-in day and time, updates the `weekly-check-in` schedule, and resumes it. It offers the monthly and quarterly reviews and resumes them only on a yes. Default crons are only sensible starting points (Sunday 18:00; 1st of the month 10:00; 1 Jan / Apr / Jul / Oct 10:00, in the install timezone).

```bash
ncl tasks list --group <group-id> --status paused
ncl tasks resume --id <series-id> --group <group-id>
```

## Services and credentials

| Tool | Setup | Where |
|------|-------|-------|
| Web search | Provided by the runtime; used for hazard maps, official alert apps, emergency numbers and civil-protection pages | no per-household setup |
| `osm` (optional) | [`osm-mcp`](https://www.npmjs.com/package/osm-mcp) 0.3.1, pinned in `mcp.json`. OpenStreetMap geocoding, nearby points of interest, foot/bike/car routes and isochrones. Public Nominatim, Overpass and OSRM endpoints, no account. | nothing to connect; the sandbox needs outbound access to the OSM endpoints. Remove the server from `mcp.json` if you'd rather not have it |

No API keys live in this template and none are needed. No paid services. `osm-mcp` accepts an optional `ORS_API_KEY` to switch routing to OpenRouteService; Wren does not use it and the template does not declare it. The public OSM endpoints have fair-use limits (roughly one request per second); Wren makes a handful of calls per onboarding and per quarterly review, which is well within them.

## Sources

Bundesamt für Bevölkerungsschutz und Katastrophenhilfe, "Vorsorgen für Krisen und Katastrophen", 2nd edition 11/2025, bbk.bund.de/vorsorge. FEMA, ready.gov/plan, ready.gov/kit, ready.gov/alerts, ready.gov/disability. Both are public guidance; the template paraphrases their lists and points to the originals for the full text.
