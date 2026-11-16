# India EV Charging Stations - a single merged dataset

A deduplicated, geo-located dataset of **28,553 public EV charging stations across India**, compiled from nine independent sources and reconciled into one record per site. Every station carries coordinates; 14,857 are confirmed by two or more sources.

**Live map: [ev.reclaim.city](https://ev.reclaim.city)** - **Interactive dashboard: [reclaimchennai.github.io/india-ev-charging-dataset](https://reclaimchennai.github.io/india-ev-charging-dataset/)**

![India EV charging map](images/site-map.jpg)

Compiled 16 November 2026 - 28,553 stations - 34 states and union territories - 223 operators - 9 sources.

---

## What is in here

| File | Rows | Description |
|------|------|-------------|
| [`data/charging_stations.csv`](data/charging_stations.csv) | 28,553 | The full dataset, one row per station. |
| [`data/charging_stations.json`](data/charging_stations.json) | 28,553 | The same records as JSON, with structured connector arrays. |
| [`dashboard.html`](dashboard.html) | - | A self-contained analytics dashboard. Also [live here](https://reclaimchennai.github.io/india-ev-charging-dataset/). |

The dashboard is also published as pictures and tables below.

### Column reference (CSV)

| Column | Meaning |
|--------|---------|
| `name` | Station name as published by the source. |
| `operator` | Charge-point operator / network brand. |
| `network` | Platform or back-end the station runs on, where known. |
| `state`, `district`, `city` | Administrative location (state/district assigned by point-in-polygon against India admin boundaries). |
| `address`, `postcode` | Street address where published. |
| `lat`, `lng` | WGS84 coordinates. Present for 100% of rows. |
| `connectors` | Connector types with power/count, e.g. `CCS2@60kW; Type2@7kW`. |
| `max_power_kw` | Peak power at the station, where published. |
| `ac_points`, `dc_points`, `n_points` | Charge-point (gun) counts by current, where published. |
| `access` | Access codes (public / restricted) as provided by the source. |
| `pricing` | Tariff string where published, e.g. `Rs 14/kWh`. |
| `phone`, `url` | Contact details where published. |
| `sources` | Which sources list this station (after dedup), e.g. `MG eHUB; Ather Grid`. |
| `n_sources` | Number of independent sources that list it. |
| `last_updated` | Most recent source timestamp for the record. |

Power, connector and tariff detail is present for roughly 49% of stations - the two large aggregator feeds and Ather Grid are location-only and do not publish it. Those figures describe only the stations that report it.

---

## Sources

Nine independent sources were merged. Each is attributed; see [SOURCES.md](SOURCES.md).

| Source | Type | Stations listed |
|--------|------|-----------------|
| Kia / Numocity | Aggregator platform | 17,239 |
| MG eHUB | Operator app network | 10,558 |
| ChargeZone | Aggregator platform | 9,288 |
| Ather Grid | Operator app network (OEM) | 3,472 |
| Bolt.Earth | Operator app network | 3,270 |
| OpenChargeMap | Community, open API | 1,847 |
| OpenStreetMap | Crowd-sourced, Overpass | 536 |
| BESCOM EV Mithra | State-utility app (Karnataka) | 192 |
| MeeTicket | State vendor (Telangana) | 77 |

Sites overlap across sources, so the listed counts sum to more than the merged total. 52,691 raw records collapsed to 28,553 unique stations - 24,138 duplicates and out-of-scope records removed by spatial deduplication and cleaning.

---

## The dataset at a glance

### How it compares to the official national count

Government counts of operational Public Charging Stations (PCS): 16,348 at March 2024 (BEE), about 26,367 by April 2025, and 29,277 by mid-2025 (Ministry of Power). This dataset finds **28,553** - about 98% of the mid-2025 figure, above the April-2025 count, and above the March-2024 count in 29 of 34 states.

![Coverage vs official count](images/dashboard-reality-check.png)

### Where the stations are

Maharashtra leads, followed by Karnataka, Tamil Nadu and Uttar Pradesh. The top eight states hold roughly two-thirds of all chargers.

| State / UT | Stations | Per million people | Official PCS (Mar 2024) |
|------------|---------:|-------------------:|------------------------:|
| Maharashtra | 4,014 | 31.5 | 3,083 |
| Karnataka | 2,735 | 40.1 | 5,130 |
| Tamil Nadu | 2,597 | 33.7 | 643 |
| Uttar Pradesh | 2,402 | 10.1 | 583 |
| Gujarat | 1,924 | 26.6 | 476 |
| Kerala | 1,845 | 51.4 | 958 |
| Rajasthan | 1,800 | 22.0 | 500 |
| Telangana | 1,676 | 43.8 | 483 |
| Madhya Pradesh | 1,327 | 15.2 | 341 |
| Haryana | 1,269 | 41.5 | 377 |
| Andhra Pradesh | 1,205 | 22.6 | 327 |
| NCT of Delhi | 883 | 40.6 | 1,886 |
| West Bengal | 800 | 8.0 | 318 |
| Punjab | 775 | 25.3 | 158 |
| Odisha | 655 | 14.1 | 198 |

The full 34-row table (every state and UT, with per-capita density) is in the dashboard:

![Every state and UT](images/dashboard-state-table.png)

### Operators

223 distinct operators appear. The leaders split into oil PSUs (near-100% DC, flat Rs 14/kWh), conglomerates (Tata, Jio-bp, Adani) and pure-play CPOs (ChargeZone, Statiq, Bolt). Ather Grid, the scooter maker's own fast-charge network, is now the second-largest by site count; its locator publishes location only, so its power and tariff fields are mostly blank. ChargeZone's station count is an upper bound - its B2C app aggregates roaming partners.

| Operator | Type | Stations | Guns | DC share | Median kW | Rs/kWh | States |
|----------|------|---------:|-----:|---------:|----------:|-------:|-------:|
| ChargeZone | Pure-play CPO | 8,020 | 2,160 | 39% | 60 | 22 | 34 |
| Ather Grid | Pure-play CPO | 3,046 | 86 | 67% | 25 | - | 27 |
| Statiq | Pure-play CPO | 2,405 | 1,031 | 92% | 60 | 23 | 30 |
| Tata Power | Conglomerate | 2,388 | 4,735 | 63% | 25 | 21 | 30 |
| HPCL eCharge | PSU oil | 2,197 | 4,101 | 98% | 30 | 14 | 27 |
| Bolt.Earth | Pure-play CPO | 2,069 | 2,439 | 80% | 3.3 | - | 23 |
| eDrive BPCL | PSU oil | 1,231 | 2,001 | 99% | 30 | 14 | 25 |
| Jio-bp Pulse | Conglomerate | 1,128 | 4,844 | 51% | 60 | 24 | 27 |
| Adani Total Energies | Conglomerate | 864 | 985 | 71% | 30 | 26 | 26 |
| EFi | Pure-play CPO | 570 | 20 | 34% | 3.3 | - | 29 |

![Operators](images/dashboard-operators.png)

### Speed, capacity and connectors

Among stations that publish power, DC fast (25-60 kW) dominates, built around the CCS2 connector. Of 34,435 charge points whose current type is published, 62% are DC.

![Speed, capacity and connectors](images/dashboard-speed-connectors.png)

### Tariffs

Across 10,429 priced stations the median is Rs 21/kWh. The distribution is bimodal: a wall at exactly Rs 14 (the subsidised oil-PSU tariff) and a private-CPO market at Rs 21-26.

![Tariffs](images/dashboard-tariffs.png)

### Provenance

![Provenance](images/dashboard-provenance.png)

---

## Method

- **Merge.** 52,691 raw records collapsed to 28,553 by spatial deduplication: sites within 150 m treated as one when closer than 75 m or when name/operator agree; every non-null field and connector kept from the richest source.
- **Cleaning.** Junk power values nulled (ceiling 400 kW), test and commissioning units removed, and a small number of out-of-land or out-of-country coordinates relocated or dropped against India admin boundaries.
- **Geocoding of admin units.** State and district assigned by point-in-polygon against India administrative boundaries.
- **Cross-verification.** 14,857 stations (52%) appear in two or more independent sources.

### Caveats

- Power, connector and tariff detail is missing for about 51% of stations (the two aggregator feeds and Ather Grid are location-only).
- ChargeZone's total includes B2C roaming aggregation and is an upper bound.
- `status` and tariff fields are point-in-time snapshots from each source.
- Counts are stations (sites), not individual guns, unless a column says otherwise.
- Per-capita figures use IIPS district population projections (2024) and exclude states under 1 million people.

---

## License and attribution

Data is released under the **Open Database License (ODbL) 1.0** (see [LICENSE](LICENSE)). You may share and adapt it, with attribution, and must keep derivative databases open under the same terms.

Attribution: *EV Charge India dataset - ev.reclaim.city*, incorporating data from MG eHUB, BESCOM EV Mithra, ChargeZone, Kia/Numocity, Ather Grid, Bolt.Earth, OpenChargeMap (openchargemap.org), OpenStreetMap (OpenStreetMap contributors, ODbL) and MeeTicket. Official counts from data.gov.in / BEE / Ministry of Power. Population from IIPS projections.

### How to cite

> EV Charge India (2026). *India EV Charging Stations - a merged dataset of 28,553 public charging stations.* ev.reclaim.city.

Maintained by Reclaim Chennai. Issues and corrections welcome.
