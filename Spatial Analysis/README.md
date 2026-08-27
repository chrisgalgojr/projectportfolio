# Organic Farming Across Europe

A spatial analysis of organic agriculture as a share of utilised
agricultural area in EU member states, built in R with Quarto and `sf`.

**Business question:** Where does organic farming concentrate, how fast
is each country moving, and which countries will miss the EU Farm to
Fork target of 25% organic land by 2030?

## Key findings

1. Organic share clusters geographically rather than distributing
   evenly across member states.
2. Most member states sit well below the 25% target in the latest
   reporting year.
3. Growth rates, not current levels, determine which countries can
   still reach the target; linear extrapolation shows few will.

Full analysis and code: [`analysis.qmd`](analysis.qmd)

## How to reproduce

```r
install.packages(c("eurostat", "sf", "giscoR", "tidyverse",
                   "scales", "knitr"))
```

```bash
quarto render analysis.qmd
```

Data download directly from the Eurostat API on first render. No
credentials required.

## Methods

- Data: Eurostat SDG indicator `sdg_02_40`, organic area as a
  percentage of utilised agricultural area.
- Boundaries: NUTS 2016 geometries from Eurostat GISCO.
- Projection: EPSG:3035 (ETRS89-LAEA), the EU standard equal-area
  projection, applied before mapping so country areas compare fairly.
- Join quality reported explicitly; unmatched geographies shown in grey
  rather than dropped silently.

## Limitations

Certified organic area excludes uncertified low-input practices.
Country-level aggregation hides regional variation. Projections assume
linear growth and no policy change. Spatial clustering is described
visually, not tested statistically; a Moran's I test is the next step.

## Data source and attribution

Eurostat, accessed via the `eurostat` R package.
Administrative boundaries © EuroGeographics.
Eurostat encourages free re-use of its data for commercial and
non-commercial purposes.

## About

Built by Christopher Jr Galgo
Contact: chris.galgo1@gmail.com
