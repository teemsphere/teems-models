# teems-models

Model files for the [Trade and Environment Equilibrium Modeling System (TEEMS)](https://teemsphere.github.io/). Each directory contains a TABLO model specification (`.tab`) and a standard closure file (`.cls`) vetted for use with the [`teems`](https://github.com/teemsphere/teems) R package.

All GTAP models carry the same small set of TEEMS modifications to the official files: sluggish and sector-specific endowments are declared explicitly instead of read from the endowment flags, the `VERNUM` version stamp is dropped, and the standard `.sti` condensation is written into the file as `Backsolve` statements, so the model condenses automatically unless loaded with `ignore_condense = TRUE`.

## Models

### GTAPv6 — GTAP Version 6.2

| | |
|---|---|
| **Type** | Static |
| **Date** | September 2003 (TEEMS modifications September 2026) |
| **Files** | `GTAPv6.tab`, `GTAPv6.cls` |

The [classic GTAP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=2458), version 6.2: multiple margin sectors, the CDE regional household demand system, welfare decomposition, import-augmenting technical change and Baldwin-type capital accumulation effects. `PROD_COMM` is read from the sets file so that a single sectoral mapping suffices.

**References:**
- Hertel, T.W. and M.E. Tsigas, "Structure of the Standard GTAP Model", Chapter 2 in T.W. Hertel (ed.) *Global Trade Analysis: Modeling and Applications*, Cambridge University Press, 1997.
- McDougall, R.A., "A New Regional Household Demand System for GTAP", GTAP Technical Paper #20, Center for Global Trade Analysis, Purdue University.
- Hertel, T.W., K. Itakura and R.A. McDougall, "GTAP.TAB: The Standard GTAP Model", GTAP Technical Paper, Center for Global Trade Analysis, Purdue University.

### GTAPv7 — GTAP Version 7.1

| | |
|---|---|
| **Type** | Static |
| **Date** | August 2023 (TEEMS modifications September 2026) |
| **Files** | `GTAPv7.tab`, `GTAPv7.cls` |

The [standard GTAP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=6438), version 7.1: activity-specific factor income taxes, endowment type flags, a refined welfare decomposition, aggregate demand and world GDP indices, and the post-simulation welfare (WELVIEW), volume (GTAPVOL) and accounting (GTAPSUM) reports.

**References:**
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-AEZ — GTAP-AEZ on GTAPv7.1

| | |
|---|---|
| **Type** | Static, land use by agro-ecological zone |
| **Date** | January 2024 AEZ layer on the version 7.1 core (TEEMS modifications September 2026) |
| **Files** | `GTAP-AEZ.tab`, `GTAP-AEZ.cls` |

The [GTAP-AEZ model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=7274): land disaggregated into agro-ecological zones and supplied to crop, grazing and forestry through a nested CET structure, with land-cover accounting and yield calibration. It runs on the GTAP-AEZ database (GTAP 11/12 AEZ releases), which `ems_data()` prepares for it.

**References:**
- Baldos, U.L.C. and E.L. Corong. "Development of GTAP version 10 Land Use and Land Cover Data Base for years 2004, 2007, 2011 and 2014." GTAP Research Memorandum No. 36, Center for Global Trade Analysis, Purdue University, 2020.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-E — GTAP-E on GTAPv7.1

| | |
|---|---|
| **Type** | Static, energy substitution and carbon emissions |
| **Date** | August 2023 energy layer on the version 7.1 core (TEEMS modifications September 2026) |
| **Files** | `GTAP-E.tab`, `GTAP-E.cls` |

The [GTAP-E model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=1668): energy commodities enter a capital-energy composite with substitution between coal, oil, petroleum products, gas and electricity; CO2 emissions are tracked by source, and carbon taxes may be levied over regional trading blocs. It runs on the GTAP-E database (GTAP 11c and 12a E releases), which `ems_data()` prepares for it. The aggregation must keep the energy commodities distinct, or the energy nest has nothing to substitute between.

**References:**
- Corong, E.L. and A. Golub. "The GTAP-E Version 7 Model: An Energy-Environmental Version of the GTAP Model." Center for Global Trade Analysis, Purdue University, 2024.
- Burniaux, J.-M. and T.P. Truong. "GTAP-E: An Energy-Environmental Version of the GTAP Model." GTAP Technical Paper No. 16, Center for Global Trade Analysis, Purdue University, 2002.
- McDougall, R. and A. Golub. "GTAP-E: A Revised Energy-Environmental Version of the GTAP Model." GTAP Research Memorandum No. 15, Center for Global Trade Analysis, Purdue University, 2007.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-EP — GTAP-E with GTAP-Power on GTAPv7.1

| | |
|---|---|
| **Type** | Static, energy substitution, electricity technologies and carbon emissions |
| **Date** | August 2023 energy and power layer on the version 7.1 core (TEEMS modifications September 2026) |
| **Files** | `GTAP-EP.tab`, `GTAP-EP.cls` |

GTAP-E with the GTAP-Power electricity detail: transmission and distribution plus eleven generation technologies in a nest that separates base-load from peak-load generation. It runs on the GTAP-Power database (GTAP 11c and 12a Power releases), which `ems_data()` prepares for it. Use the shipped `power` and `power_tech` mappings: merging a base-load with a peak-load technology makes the generation nest ill-defined.

**References:**
- Peters, J.C. "GTAP-E-Power: An Electricity-detailed Economy-wide Model." *Journal of Global Economic Analysis*, 1(2), 156-187, 2016.
- Peters, J.C. "The GTAP-Power Data Base: Disaggregating the Electricity Sector in the GTAP Data Base." *Journal of Global Economic Analysis*, 1(1), 209-250, 2016. https://doi.org/10.21642/JGEA.010104AF
- Corong, E.L. and A. Golub. "The GTAP-E Version 7 Model: An Energy-Environmental Version of the GTAP Model." Center for Global Trade Analysis, Purdue University, 2024.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-RE — GTAP-RE Version 2

| | |
|---|---|
| **Type** | Intertemporal with rational expectations |
| **Date** | September 2026 (Version 1: May 2025) |
| **Files** | `GTAP-RE.tab`, `GTAP-RE.cls` |

An intertemporal rational expectations extension of GTAPv7.1: the version 7.1 core indexed over time, with a convex-adjustment-cost investment function, capital accumulation and a present-value rational expectations mechanism. It carries no backsolves, since condensation densifies the block structure the intertemporal matrix methods rely on.

GTAP-INT, the earlier intertemporal extension of GTAPv6.2, is deprecated in favour of GTAP-RE.

**References:**
- Van Ha, P., T. Kompas, and M. Cantele. "Rethinking the Solution Strategy for Large Recursive CGE Models: Solving Recursive and Rational Expectations CGE Models the Non-Recursive Way." Unpublished manuscript, University of Melbourne.
- Van Ha, P. and T. Kompas, "Solving intertemporal CGE models in parallel using a singly bordered block diagonal ordering technique." *Economic Modelling*, 52, 3-12, 2016. https://doi.org/10.1016/j.econmod.2015.07.011
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### ORANI-G — ORANI-G 2013 edition

| | |
|---|---|
| **Type** | Static, single country (Australia, 37 commodities, 35 industries) |
| **Date** | August 2013 |
| **Files** | `ORANI-G.tab`, `ORANI-G.cls`, `ORANI-G-LR.cls` |

The [ORANI-G model](https://www.copsmodels.com/oranig.htm), the generic single-country model of the Centre of Policy Studies. The only modification declares the investment-rule sets `EXOGINV` and `ENDOGINV` in the model file so that the closures can refer to them. It loads its `basedata.har` with `ems_data("basedata.har")`. `ORANI-G.cls` is the short-run closure, `ORANI-G-LR.cls` the long-run one.

**References:**
- Horridge, M. "ORANI-G: A Generic Single-Country Computable General Equilibrium Model." Centre of Policy Studies and Impact Project, Monash University, 2003 (model files: 2013 edition).
- Dixon, P.B., B.R. Parmenter, J. Sutton and D.P. Vincent. *ORANI: A Multisectoral Model of the Australian Economy*. North-Holland, Amsterdam, 1982.

## Usage

```r
model <- ems_model(
  model_file = "path/to/GTAPv7.tab",
  closure_file = "path/to/GTAPv7.cls"
)
```

## Attribution

The GTAP modeling framework is developed and maintained by the [Center for Global Trade Analysis](https://www.gtap.agecon.purdue.edu/), Purdue University. The intertemporal extensions (GTAP-INT, GTAP-RE) were developed by Pham Van Ha and Tom Kompas at the University of Melbourne. ORANI-G is developed and maintained by the [Centre of Policy Studies](https://www.copsmodels.com/), Victoria University (formerly Monash University). TEEMS-compatible syntactic modifications were made by Matthew Cantele.
