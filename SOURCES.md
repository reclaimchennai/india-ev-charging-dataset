# Sources and attribution

This dataset merges nine independent public sources of EV charging station locations in India. Each record keeps the richest field available across the sources that list it, and records the sources in the `sources` column. Counts below are stations listed by each source before deduplication; sites overlap, so they sum to more than the 28,553 merged total.

| # | Source | What it is | Attribution / license |
|---|--------|-----------|-----------------------|
| 1 | **Kia / Numocity** | Aggregator charge-point locator covering many operators | Kia India / Numocity, public listing |
| 2 | **MG eHUB** | Operator app network | MG Motor / eHUB, public listing |
| 3 | **ChargeZone** | Aggregator platform (includes several partner networks) | ChargeZone, public listing |
| 4 | **Ather Grid** | OEM-operated public fast-charge network (Ather Energy) | Ather Energy, public listing |
| 5 | **Bolt.Earth** | Operator app network (dense two- and three-wheeler charging) | Bolt.Earth, public listing |
| 6 | **OpenChargeMap** | Community open database | (c) OpenChargeMap contributors, openchargemap.org, CC BY-SA / open API |
| 7 | **OpenStreetMap** | Crowd-sourced map data (`amenity=charging_station`) | (c) OpenStreetMap contributors, ODbL, openstreetmap.org |
| 8 | **BESCOM EV Mithra** | Karnataka state-utility charging app | BESCOM, public listing |
| 9 | **MeeTicket** | Telangana state charging vendor | MeeTicket / Telangana, public listing |

## Reference data (not charging locations)

- **Official PCS counts** used for comparison: data.gov.in / Bureau of Energy Efficiency (March 2024), parliamentary reply (April 2025), Ministry of Power (mid 2025).
- **Population** for per-capita figures: IIPS district population projections (2024).
- **Administrative boundaries** (for state/district assignment): India state boundaries, GADM.

## How the merge works

The processing is spatial and deterministic:

1. **Normalise** each source into a common schema (name, operator, coordinates, connectors, power, pricing, access).
2. **Deduplicate** spatially: stations within 150 m are treated as one site when they are closer than 75 m, or when name/operator agree. The merged record keeps every non-null field and all distinct connectors.
3. **Clean**: null out impossible power values (ceiling 400 kW), remove test and commissioning units, and relocate or drop a small number of coordinates that fall outside India's land boundary.
4. **Assign** state and district by point-in-polygon against India administrative boundaries.

This repository publishes the resulting dataset and its summary analytics. It does not document the collection tooling.

## Corrections

The dataset is a snapshot and will contain errors - wrong coordinates, stale status, duplicate sites that slipped the spatial match. Corrections are welcome via the repository issue tracker. A share of stations (52%) is cross-verified by two or more sources, which is the first reliability signal before a site is physically checked.
