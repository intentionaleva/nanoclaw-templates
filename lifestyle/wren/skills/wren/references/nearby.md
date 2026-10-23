# Nearby places (optional `osm` server)

The `osm` MCP server (osm-mcp, OpenStreetMap, no key) adds real places to the plan: where the nearest pharmacy, hospital, fire station, police station and emergency shelter are, how far on foot, and whether a chosen meeting place is actually reachable. Use it when it is present; if its tools are missing, skip this reference and say in one line that place lookups aren't connected.

Tools you'll use: `geocode` (address to coordinates, once per location at onboarding; store the coordinates in `prep/profile.md`), `find_nearby_pois` (by category or OSM tag), `route` (foot, bike, car) and `isochrone` (how far you get in 15 minutes on foot).

## Where it goes in the plan

- **Onboarding, after block 2.** Geocode home and each regular location. No chat output needed beyond "noted".
- **Risk pass.** For home: nearest `amenity=hospital`, `amenity=pharmacy`, `amenity=fire_station`, `amenity=police`, and anything tagged `emergency=shelter` or `social_facility`. Record names and foot distances in `prep/risks.md` under "Nearby help". Also check `man_made=works`, `industrial=chemical`, `power=plant` with `plant:source=nuclear` within 10 km as a cross-check for the industrial line, but the official Störfall/EPZ page stays the source; OSM only points you at what to verify.
- **Communication card.** Propose the three meeting places from real candidates: meeting 1 is a landmark within 100 m of home (a tree, a lamp post, a bus stop); meeting 2 is a public place within the 15-minute foot isochrone (school, church, supermarket car park); meeting 3 is out of town, usually a relative's address. Route each on foot from home and from school or work, and state the minutes. Check the route works for anyone with a mobility aid (no stairs-only paths; say if you can't tell).
- **Travel pass.** Nearest hospital and pharmacy to the accommodation; put them on the travel card.
- **Quarterly review.** Re-check the nearby list; shops and pharmacies close.

## Rules

- OSM is community data and can be out of date. Say "according to OpenStreetMap" and tell the household to confirm opening hours and emergency status with the municipality. A pharmacy on the map is a lead, not a promise.
- Never use OSM for a hazard likelihood. The official map is the source; OSM only helps find what to verify.
- Keep output short: name, type, distance on foot. Three to five places, not twenty.
- Coordinates and addresses are personal data; they live in `prep/` only.
