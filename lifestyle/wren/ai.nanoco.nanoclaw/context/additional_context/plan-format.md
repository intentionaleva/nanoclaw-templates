# File formats under `prep/`

Keep these exact shapes so every check-in and review reads the same structure.

## prep/profile.md

```markdown
# Household profile
updated: 2026-10-23

## People
| name | age band | role | needs |
|------|----------|------|-------|
| Eva  | adult    | lead | none  |
| Tom  | toddler  |      | nappies, formula?, pram |

age band: infant / toddler / child / teen / adult / senior

## Pets
| name | species | food/day | meds |

## Locations
| label | where (town, postcode) | type | floor | cellar | heating | car |
|-------|------------------------|------|-------|--------|---------|-----|
| home  | …                      | flat/house | … | yes/no | gas/oil/heat pump/district | yes/no |
| work  | … | | | | | |
| daycare / school | … | | | | | |

## Travel (next 12 months)
| when | where | with whom |

## Medical and access needs
- (one line per person: medication name not required; "daily prescription, 10-day reserve needed", "hearing aid", "wheelchair", "insulin, needs cooling")

## Language, alerts, numbers
- language:
- country:
- official alert app:
- emergency numbers:

## Goal
basics (3 days) / solid (10 days) / max (30+ days, off-grid comms and power)

## Budget
one-off: € … | monthly: € … | hard ceiling: yes/no

## Already in place
- (what they told you they have; no inference)

## Check-in cadence
weekly on <day> at <time>; monthly kit review: yes/no; quarterly review: yes/no
```

## prep/risks.md

```markdown
# Risks
checked: 2026-10-23

## home (Lindlar, 51789)
| hazard | likelihood | evidence | source | checked |
|--------|------------|----------|--------|---------|
| river flooding | low | not in HQ100 zone | NRW Hochwassergefahrenkarte (link) | 2026-10-23 |
| power cut >24h | moderate | rural grid, storm history | Netzbetreiber Störungsmeldungen; DWD | 2026-10-23 |
| winter storm | moderate | DWD climate record for the Oberbergisches Land | DWD (link) | 2026-10-23 |

## work (…)
…

## travel: Gran Canaria, Jan 2027
| hazard | note | source |
```

likelihood: low / moderate / high. Only "high" when an official map or authority says so.

## prep/plan.md

```markdown
# Plan
goal: solid (10 days) | budget: €300 one-off, €30/month | started: 2026-10-23

## Red (this week)
| # | item | why | cost band | owner | due | status |
|---|------|-----|-----------|-------|-----|--------|
| R1 | Install NINA, enable alerts for Lindlar | official warnings | €0 | Eva | 2026-10-25 | open |
| R2 | Comms card: out-of-area contact, meeting points | family may be apart | €0 | Eva | 2026-10-26 | open |

## Amber (next 4–8 weeks)
| # | item | why | cost band | owner | due | status |

## Green (3–12 months)
| # | item | why | cost band | owner | due | status |

## Done
| # | item | done on |
```

cost band: €0 / € (under 50) / €€ (50–300) / €€€ (300–1,500) / €€€€ (over 1,500)
status: open / in progress / blocked / skipped / done

## prep/comms-card.md

Follow `skills/wren/references/communication-plan.md`. It mirrors the ready.gov card: household members with mobile numbers, out-of-area contact, meeting places (near home, in the neighbourhood, out of town), schools and daycare with their emergency policy, doctors, insurers, utilities, and the one-line instruction "text, don't call".

## prep/log.md

One dated line per check-in or change:

```
2026-10-30 check-in: R1 done, R2 in progress (contact chosen, card not printed), A3 skipped once (no car this week).
```
