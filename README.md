# CHANCEN Maps

A collection of GeoJSON boundary files for countries where CHANCEN members are active. These files are intended for use in map visualizations, dashboards, and geographic data analysis.

## Repository Structure

```
maps/
├── el_mundo.geojson              # World countries (Natural Earth 1:10m)
├── Kenya/
│   └── kenyan-counties.geojson  # Kenya — 47 counties (ADM1)
├── Rwanda/
│   └── geoBoundaries-RWA-ADM2.geojson  # Rwanda — 30 districts (ADM2)
└── South Africa/
    └── south-africa.geojson     # South Africa — 52 municipal districts
```

## Files

### `el_mundo.geojson` — World Countries
- **Source:** Natural Earth `ne_10m_admin_0_countries` (1:10m scale)
- **Coverage:** All sovereign countries worldwide
- **Geometry:** MultiPolygon
- **CRS:** WGS84 / CRS84

### `Kenya/kenyan-counties.geojson` — Kenya Counties
- **Coverage:** All 47 counties of Kenya (ADM1 administrative level)
- **Geometry:** Polygon
- **Key properties:**
  | Property | Description |
  |---|---|
  | `COUNTY` | County name |
  | `OBJECTID` | Unique identifier |
  | `AREA` | Area (degrees²) |
  | `PERIMETER` | Perimeter length |
  | `Shape_Area` | Shape area |
  | `Shape_Leng` | Shape perimeter length |

### `Rwanda/geoBoundaries-RWA-ADM2.geojson` — Rwanda Districts
- **Source:** [geoBoundaries](https://www.geoboundaries.org/) — RWA ADM2
- **Coverage:** All 30 districts of Rwanda (ADM2 administrative level)
- **Geometry:** Polygon
- **CRS:** `urn:ogc:def:crs:OGC:1.3:CRS84`
- **Key properties:**
  | Property | Description |
  |---|---|
  | `shapeName` | District name |
  | `shapeID` | Unique geoBoundaries shape ID |
  | `shapeISO` | ISO code (where available) |
  | `shapeGroup` | Country group code (`RWA`) |
  | `shapeType` | Administrative level (`ADM2`) |

### `South Africa/south-africa.geojson` — South Africa Districts
- **Coverage:** 52 municipal districts of South Africa
- **Geometry:** MultiPolygon
- **Key properties:**
  | Property | Description |
  |---|---|
  | `name` | District name |
  | `cartodb_id` | CartoDB identifier |
  | `created_at` | Record creation timestamp |
  | `updated_at` | Record update timestamp |

## Usage

All files are standard GeoJSON (`FeatureCollection`) and can be loaded directly in any GIS tool or mapping library.

**Leaflet (JavaScript)**
```js
fetch('./Kenya/kenyan-counties.geojson')
  .then(res => res.json())
  .then(data => L.geoJSON(data).addTo(map));
```

**Mapbox GL JS**
```js
map.addSource('kenya-counties', {
  type: 'geojson',
  data: './Kenya/kenyan-counties.geojson'
});
```

**Python (GeoPandas)**
```python
import geopandas as gpd

kenya = gpd.read_file('Kenya/kenyan-counties.geojson')
rwanda = gpd.read_file('Rwanda/geoBoundaries-RWA-ADM2.geojson')
south_africa = gpd.read_file('South Africa/south-africa.geojson')
```

## Contributing

When adding a new country:
1. Place the file under a folder named after the country (e.g., `Uganda/`).
2. Use WGS84 (EPSG:4326) coordinate reference system.
3. Prettify / format the JSON before committing for readable diffs.
4. Update this README with the new file's coverage, source, feature count, and key properties.
