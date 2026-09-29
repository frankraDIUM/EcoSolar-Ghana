 # ☀️ EcoSolar-Ghana
A GeoAI-enabled decision-support for solar screening: multi-criteria suitability, spatial candidate delineation, ranking, and human review.

Savannah Region (Ghana) is the first validation study area.  
The analytical pipeline is designed to be **AOI-agnostic**,not a one-off “Savannah-only model.”

---

## Live demo

**[EcoSolar-Ghana Decision Support](https://frankradium.github.io/EcoSolar-Ghana/)**

Interactive MapLibre map · human review (pass / field check / fail) · 7-day solar weather context · optional Cesium 3D conceptual layout · CSV / JSON export.

> Reviews are stored in the browser (`localStorage`). Export JSON from **Data & Downloads** to share or back up decisions.  
> Screening support only, not a final engineering, environmental, land-tenure, or interconnection approval.

---

## Problem

Expanding renewable energy at utility scale can conflict with ecology, land use, and infrastructure reality. EcoSolar asks:

> **Where can Ghana site utility-scale solar with strong resource and access while respecting protected areas and screening out clearly unsuitable land?**

The system turns multi-source geospatial data into **ranked candidate parcels** and a **human-in-the-loop review layer**.

---

## What this project is (and is not)

| Is | Is not |
|----|--------|
| Regional **screening** and prioritisation | Final engineering design |
| Transparent multi-criteria spatial model | Black-box site generator |
| Human review of model shortlists | Automatic build approval |
| Savannah as first **validation AOI** | Finished multi-country platform |

---

## End-to-end workflow

```
RAW GEOSPATIAL DATA
        ↓
Standardised layers
  (solar · terrain · land cover · protected areas · roads · grid)
        ↓
Multi-criteria suitability surface
        ↓
Candidate landscapes  (≥50 envelope; ≥55 anchors)
        ↓
Practical parcels
  (core-driven · residual_55 · residual_oversized)
        ↓
Site metrics + composite ranking
        ↓
Desktop / field-oriented validation
        ↓
Decision-support interfaces
  Streamlit prototype  ·  GitHub Pages web app
```
## Analytical pipeline (completed)
Data layers


| Layer        | Role                                           |
| ------------ | ---------------------------------------------- |
| AOI          | Ghana ADM1 → Savannah Region                   |
| Solar        | Global Solar Atlas GHI (+ NASA POWER check)    |
| Terrain      | DEM → slope / terrain suitability              |
| Land cover   | ESA WorldCover → development suitability score |
| Ecology      | WDPA protected areas → hard exclusion          |
| Roads        | OSM-derived accessibility score                |
| Transmission | Africa grid (Ghana) → grid proximity score     |

Layers are aligned to a common analysis grid (~30.6 m, UTM) for overlay.
Suitability model (v0.1)
Factors (higher = better; illustrative weights):

| Factor             | Weight |
| ------------------ | ------ |
| Solar potential    | 35%    |
| Terrain            | 15%    |
| Land cover         | 15%    |
| Road accessibility | 15%    |
| Grid proximity     | 20%    |

Constraint: protected areas are hard-excluded from the suitability surface.

Parcels and ranking

Contiguous candidate parcels in an operational 50–200 ha band
50 ha = viability floor · 200 ha = ceiling (not targets)
Parcel sources: core · residual_55 · residual_oversized
Composite rank score (suitability + grid + road access)
Site product includes WGS84 representative points for navigation / Maps

Validation highlights

Imagery review of top candidates
Polygon-level land-cover and ecological-constraint checks
Hard fails for clear settlement risk (e.g. high built-up share)
Field-check flags for boundary, cropland, or pin/imagery uncertainty

## Key achievements

- Full screening chain: multi-source GIS → suitability → parcels → ranked sites
- Explicit energy–ecology framing via protected-area hard exclusion
- Parcel logic refined to prioritise contiguous, natural extents over quota-driven extraction
- AOI-agnostic module design (Savannah as configuration, not hard-coded identity)
- Human-in-the-loop review separated from model ranking
