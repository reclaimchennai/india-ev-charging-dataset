# Data files

- **charging_stations.csv** - 25,587 rows, one per station. Connector detail is flattened into the `connectors` column as `type@powerkW` segments separated by `; `.
- **charging_stations.json** - the same records with `connectors` as an array of `{type, power_kw, current, count}` objects, plus `ac_points` / `dc_points` / `n_points`.

Both are UTF-8. Coordinates are WGS84. See the repository README for the full column reference, sources and license.
