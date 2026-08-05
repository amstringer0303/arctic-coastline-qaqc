# Arctic Coastline Exposure QA/QC

Interactive, click-through classification tool for manually assessing coastal
exposure/shelter across 66 landfast-ice-monitored Arctic coastal communities,
paired with data-driven bathymetry computed over each community's actual
observed landfast-ice footprint.

## Contents

- **`index.html`** — the classification tool. Open directly in a browser
  (no server needed). For each community it shows three toggleable views
  (Regional bathymetry / Local high-res bathymetry / Satellite imagery),
  independently zoomable and pannable, alongside a data-driven bathymetry
  summary panel. Labels persist locally (`localStorage`) and export to CSV.

  > Note: the ~200 background PNG tiles (regional/local/satellite × 66
  > communities, ~200MB total) that `index.html` loads are **not** included
  > in this repo due to size — the tool will show broken images without
  > them. Ask for that folder separately if you need to actually run it
  > elsewhere.

- **`community_analysis.csv`** — master per-community data table: ice area,
  extent, coastline complexity, and bathymetry metrics, including:
  - `Mean Depth Under Ice (m)`, `Frac <20m Under Ice`, `Frac <2m Under Ice`,
    `Frac >100m Under Ice` — computed by rasterizing each year's fast-ice
    polygon (CIS/NIC charts) onto GEBCO bathymetry and sampling depth only
    within the ≥50%-of-years ice-covered footprint, so mean depth and the
    depth-bin fractions are guaranteed to come from the same mask (fixes an
    earlier inconsistency in the legacy `Mean Depth Ice Extent (m)` /
    `Frac <20m` columns, which were computed over two different,
    undocumented reference areas).
  - `Basin Depth (m)` — maximum bathymetric depth in the wider 50×50km site
    window (not ice-mask-restricted).

## Exposure categories (manual, in `index.html`)

Extremely exposed · Lightly exposed · Lightly sheltered · Extremely
sheltered · Fjords · Not sure

## Depth categories (data-driven, in `community_analysis.csv` / `index.html`)

Tertiles of the 66-community `Mean Depth Under Ice` distribution: Shallow
(<15.5m) · Moderate (15.5–47.0m) · Deep (≥47.0m). The separate
`Frac <20m Under Ice` fraction stat uses a fixed 20m threshold from the
landfast-ice grounding/ridging literature (Mahoney et al. 2007, JGR; Mahoney
2006), independent of this dataset's own distribution.

---
This repository contains unpublished research data. Please do not
redistribute without permission.
