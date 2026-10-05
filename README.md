# teems-models

Model files for the [Trade and Environment Equilibrium Modeling System (TEEMS)](https://teemsphere.github.io/). Each directory contains a TABLO model specification (`.tab`) and a standard closure file (`.cls`) vetted for use with the [`teems`](https://github.com/teemsphere/teems) R package.

## Models

### GTAPv6 — GTAP Version 6.2

| | |
|---|---|
| **Type** | Static |
| **Date** | September 2003 (TEEMS modifications September 2026) |
| **Files** | `GTAPv6.tab`, `GTAPv6.cls` |

The [classic GTAP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=2458), version 6.2. Includes multiple margin sectors, the CDE regional household demand system, welfare decomposition, import-augmenting technical change, and Baldwin-type capital accumulation effects.

TEEMS modifications relative to the official `gtap.tab`: sluggish endowments are declared explicitly (`land`, `natlres`) rather than read from the `SLUG` parameter; `PROD_COMM` is read from the sets file (with `CGDS_COMM` declared and `TRAD_COMM` derived) so that a single sectoral mapping suffices; `ETRAE` is declared over `ENDWS_COMM`; the `VERNUM` version stamp is dropped; and the standard `gtap.sti` condensation (9 omissions, 60 backsolves) is written into the file as `Omit`/`Backsolve` statements, so the model condenses automatically unless loaded with `ignore_condense = TRUE`.

**References:**
- Hertel, T.W. and M.E. Tsigas, "Structure of the Standard GTAP Model", Chapter 2 in T.W. Hertel (ed.) *Global Trade Analysis: Modeling and Applications*, Cambridge University Press, 1997.
- McDougall, R.A., "A New Regional Household Demand System for GTAP", GTAP Technical Paper #20, Center for Global Trade Analysis, Purdue University.
- Hertel, T.W., K. Itakura and R.A. McDougall, "GTAP.TAB: The Standard GTAP Model", GTAP Technical Paper, Center for Global Trade Analysis, Purdue University.

### GTAPv7 — GTAP Version 7.0

| | |
|---|---|
| **Type** | Static |
| **Date** | August 2023, version 7.1 (TEEMS modifications September 2026) |
| **Files** | `GTAPv7.tab`, `GTAPv7.cls` |

The [standard GTAP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=6438), version 7.1 (the August 2023 release of the version 7 file). Supersedes version 6.2 with activity-specific factor income taxes, endowment type flags, refined welfare decomposition distinguishing output and income tax effects, aggregate demand quantity indices, world GDP indices, and the post-simulation welfare-decomposition (WELVIEW), volume (GTAPVOL) and accounting-check (GTAPSUM) reports.

TEEMS modifications relative to the official `gtapv7.tab`: sluggish and sector-specific endowments are declared explicitly (`land`, `natlres`) rather than read from the `ENDOWFLAG` parameter; the `VERNUM` version stamp is dropped; and the standard `gtapv7.sti` condensation (11 omissions, 72 backsolves) is written into the file as `Omit`/`Backsolve` statements, so the model condenses automatically unless loaded with `ignore_condense = TRUE`. Everything else, including the post-simulation report blocks, is the official text.

**References:**
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-AEZ — GTAP-AEZ on GTAPv7.1

| | |
|---|---|
| **Type** | Static, land use by agro-ecological zone (based on GTAPv7.1) |
| **Date** | January 2024 AEZ layer on the August 2020 version 7.1 core (TEEMS modifications September 2026) |
| **Files** | `GTAP-AEZ.tab`, `GTAP-AEZ.cls` |

The [GTAP-AEZ model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=7274): the standard GTAP model with land disaggregated into agro-ecological zones (AEZ), land supplied to crop, grazing and forestry activities through a nested constant-elasticity-of-transformation structure, land-cover accounting (forest, pasture, cropland, unmanaged land) and yield calibration. It runs on the GTAP-AEZ database (GTAP 11/12 AEZ releases); the `teems` R package prepares that database for the model (`GTAP_convert(target = "GTAP-AEZ")`, or automatically in `ems_data()`), including the disaggregated activity sets and mapping that flexagg's `aggdat_aez.tab` synthesizes at aggregation.

TEEMS modifications relative to the official `gtapv7-aez.tab`, the same class as for GTAPv7: the sluggish endowments are declared as the AEZ land endowments (`ENDWS = AEZS`, with the `AEZS` read moved ahead of the endowment classes) and the sector-specific endowment explicitly (`natlres`) rather than read from the `ENDOWFLAG` parameter; the `VERNUM` version stamp is dropped; and the `gtapv7-aez.sti` condensation (11 omissions, 71 backsolves) is written into the file as `Omit`/`Backsolve` statements. Everything else, including the land-use set builders, the `IF` conditionals of the land equations and calibration formulas, and the post-simulation reports, is the official text.

**References:**
- Baldos, U.L.C. and E.L. Corong. "Development of GTAP version 10 Land Use and Land Cover Data Base for years 2004, 2007, 2011 and 2014." GTAP Research Memorandum No. 36, Center for Global Trade Analysis, Purdue University, 2020.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-E — GTAP-E on GTAPv7.1

| | |
|---|---|
| **Type** | Static, energy substitution and carbon emissions (based on GTAPv7.1) |
| **Date** | August 2023 energy layer on the August 2020 version 7.1 core (TEEMS modifications September 2026) |
| **Files** | `GTAP-E.tab`, `GTAP-E.cls` |

The [GTAP-E model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=1668): the standard GTAP model extended with energy substitution and carbon emissions accounting. Energy commodities leave the intermediate-input nest and enter a capital-energy composite, with substitution between coal, oil, petroleum products, gas and electricity in a nested structure; CO2 emissions are tracked by source, and carbon taxes may be levied over regional trading blocs. It runs on the GTAP-E database (the GTAP 11c and 12a E releases); the `teems` R package prepares that database for the model (`GTAP_convert(target = "GTAP-E")`, or automatically in `ems_data()`), including the disaggregated commodity set and mapping and the aggregated energy sets that flexagg's `aggdat_e.tab` synthesizes at aggregation, and the `SUBP`/`INCP` headers the model reads over `TOPP`, rebuilt from the commodity-level CDE parameters as flexagg's `aggpar_e.tab` builds them.

TEEMS modifications relative to the official `gtapv7-e.tab`, the same class as for GTAPv7: the sluggish and sector-specific endowments are declared explicitly (`ENDWS = land`, `ENDWF = natlres`) rather than read from the `ENDOWFLAG` parameter; the `VERNUM` version stamp is dropped; and the `gtapv7-e.sti` condensation (10 omissions, 96 backsolves) is written into the file as `Omit`/`Backsolve` statements. Everything else, including the energy nest set builders, the `IF` conditionals, the carbon accounting and the post-simulation reports, is the official text.

Note that the aggregation must keep the energy commodities distinct. An aggregation that merges them (for example one that maps coal, oil, gas, petroleum products, electricity and gas distribution into a single manufacturing sector) collapses the energy nest onto one element: the model still solves, but there is nothing left for it to substitute between.

**References:**
- Burniaux, J.-M. and T.P. Truong. "GTAP-E: An Energy-Environmental Version of the GTAP Model." GTAP Technical Paper No. 16, Center for Global Trade Analysis, Purdue University, 2002.
- McDougall, R. and A. Golub. "GTAP-E: A Revised Energy-Environmental Version of the GTAP Model." GTAP Research Memorandum No. 15, Center for Global Trade Analysis, Purdue University, 2007.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-EP — GTAP-E with GTAP-Power on GTAPv7.1

| | |
|---|---|
| **Type** | Static, energy substitution, electricity technologies and carbon emissions (based on GTAPv7.1) |
| **Date** | August 2023 energy and power layer on the August 2020 version 7.1 core (TEEMS modifications September 2026) |
| **Files** | `GTAP-EP.tab`, `GTAP-EP.cls` |

The [GTAP-EP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=1668): GTAP-E extended with the GTAP-Power electricity detail. The single electricity activity is replaced by transmission and distribution together with eleven generation technologies, which enter a nested structure distinguishing base-load from peak-load generation, so that the model represents substitution between generation sources as well as between fuels. It runs on the GTAP-Power database (the GTAP 11c and 12a Power releases, 76 commodities and activities); the `teems` R package prepares that database for the model (`GTAP_convert(target = "GTAP-EP")`, or automatically in `ems_data()`), synthesizing the twenty-seven set headers that flexagg builds at aggregation and the `SUBP`/`INCP` headers the model reads over `TOPP`, rebuilt from the commodity-level CDE parameters as flexagg's `aggpar_p.tab` builds them.

TEEMS modifications relative to the official `gtapv7-ep.tab`, the same class as for GTAPv7: the sluggish and sector-specific endowments are declared explicitly (`ENDWS = land`, `ENDWF = natlres`) rather than read from the `ENDOWFLAG` parameter; the `VERNUM` version stamp is dropped; and the `gtapv7-ep.sti` condensation (10 omissions, 97 backsolves) is written into the file as `Omit`/`Backsolve` statements. Everything else, including the electricity nests, the set builders, the carbon accounting and the post-simulation reports, is the official text.

Note that the aggregation must keep the electricity commodities apart. One that merges a base-load technology with a peak-load one makes the base-load and peak-load input sets overlap and the generation nest ill-defined, so the standard activity mappings cannot be used: the shipped `power` and `power_tech` mappings are built for this database.

**References:**
- Peters, J.C. "The GTAP-Power Data Base: Disaggregating the Electricity Sector in the GTAP Data Base." *Journal of Global Economic Analysis*, 1(1), 209-250, 2016. https://doi.org/10.21642/JGEA.010104AF
- Burniaux, J.-M. and T.P. Truong. "GTAP-E: An Energy-Environmental Version of the GTAP Model." GTAP Technical Paper No. 16, Center for Global Trade Analysis, Purdue University, 2002.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### ORANI-G — ORANI-G 2013 edition

| | |
|---|---|
| **Type** | Static, single country (Australia, 37 commodities, 35 industries, 8 occupations, 8 regions) |
| **Date** | August 2013 (2013 edition of the 2003 model) |
| **Files** | `ORANI-G.tab`, `ORANI-G.cls`, `ORANI-G-LR.cls` |

The [ORANI-G model](https://www.copsmodels.com/oranig.htm): the generic single-country computable general equilibrium model of the Centre of Policy Studies, with multi-product industries, margins, the linear expenditure system for households, separate export demand schedules for individual and collective exports, the DPSV investment rules, a top-down regional extension and the Fan and GDP decompositions of its post-simulation reports. It is the reference model of the CoPS Practical GE Modelling Course and the basis of many national models.

TEEMS modification relative to the official `oranig.tab`: the investment-rule industry sets `EXOGINV` and `ENDOGINV`, which the ORANIG command files declare with `xSet`/`xSubset`, are declared in the model file so that the closures can refer to them. Everything else is the official 2013 text. The `teems` R package reads its `Write (Set)` statements, the `WAGGSET` aggregation instructions and the ranked report set as described in the manual, holds the `Omit` variables exogenous, and loads its `basedata.har` through the single-file route of `ems_data()` (`ems_data("basedata.har")`, no set mappings). Two closures ship: `ORANI-G.cls` is the short-run closure of `oranigSR.CMF` (the DPSV closure, exchange rate numeraire), `ORANI-G-LR.cls` the long-run closure of `oranigLR.CMF` with that command file's swaps applied (rates of return, employment, the stock and balance-of-trade rules and the investment rules exogenous in place of capital stocks, the wage shifter, their shift variables and industry investment).

**References:**
- Horridge, M. "ORANI-G: A Generic Single-Country Computable General Equilibrium Model." Centre of Policy Studies and Impact Project, Monash University, 2003 (model files: 2013 edition).
- Dixon, P.B., B.R. Parmenter, J. Sutton and D.P. Vincent. *ORANI: A Multisectoral Model of the Australian Economy*. North-Holland, Amsterdam, 1982.

### GTAP-INT — GTAP-INT Version 1

| | |
|---|---|
| **Type** | Intertemporal (based on GTAPv6.2) |
| **Date** | January 2025 (TEEMS modifications September 2026) |
| **Files** | `GTAP-INT.tab`, `GTAP-INT.cls` |

An intertemporal extension of the GTAPv6.2 model developed by Kompas and Van Ha. Adds a time dimension for dynamic analysis with forward-looking investment and capital accumulation.

TEEMS modifications: the standard `gtap.sti` omissions (9 exogenous technical-change and tax shifters) are written into the file as an `Omit` statement. No backsolves are written in: the intertemporal system solves faster uncondensed with the bordered matrix methods. Load with `ignore_condense = TRUE` to shock an omitted variable.

**References:**
- Van Ha, P. and T. Kompas, "Solving intertemporal CGE models in parallel using a singly bordered block diagonal ordering technique." *Economic Modelling*, 52, 3-12, 2016. https://doi.org/10.1016/j.econmod.2015.07.011
- Kompas, T. and P. Van Ha, "The 'curse of dimensionality' resolved: The effects of climate change and trade barriers in large dimensional modelling." *Economic Modelling*, 80, 103-110, 2019. https://doi.org/10.1016/j.econmod.2018.08.011

### GTAP-RE — GTAP-RE Version 2

| | |
|---|---|
| **Type** | Intertemporal with rational expectations (based on GTAPv7.1) |
| **Date** | September 2026 (Version 1: May 2025) |
| **Files** | `GTAP_RE.tab`, `GTAP_RE.cls` |

An intertemporal rational expectations extension of the GTAPv7.1 model. Version 2 is the official GTAPv7.1 core (as in `GTAPv7.tab` above, post-simulation reports included) time-indexed over `ALLTIME`, with the Version 1 components spliced in: time sets read from `GTAPINT`, a convex-adjustment-cost investment function, capital accumulation over `FWDTIME` and the present-value rational expectations mechanism (`pval`, `ror_act`, the `REDELTA`/`RESEDELTA`/`REEXODELTA` switches). The Version 1 workarounds for the earlier solver are gone. Every coefficient and variable carries the time index except the model constants (`RNREG`, `NTSP`, `DELTAKADJ`, `RORDELTA`, the `RE*DELTA` switches); Version 1 left `aosec` time-invariant, Version 2 indexes it like the other shifters. There are no `Omit` or backsolve statements, since substitution densifies the block structure the intertemporal matrix methods rely on. On a three-period aggregation the two versions solve to identical results.

October 2026: the discount term of `PVALFWDTIME` is taken over the period length `Year(t+1)-Year(t)`, as in `PVALENDTIME`, so multi-year time steps discount consistently (annual steps are unchanged); the depreciation rate `KAPPA` is 0.04, the rate of the GTAP data (`VDEP`/`VKB`), in place of 0.05.

**References:**
- Van Ha, P., T. Kompas, and M. Cantele. "Rethinking the Solution Strategy for Large Recursive CGE Models: Solving Recursive and Rational Expectations CGE Models the Non-Recursive Way." Unpublished manuscript, University of Melbourne.
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

## Usage

```r
model <- ems_model(
  model_input = "path/to/GTAPv7.tab",
  closure_file = "path/to/GTAPv7.cls"
)
```

## Attribution

The GTAP modeling framework is developed and maintained by the [Center for Global Trade Analysis](https://www.gtap.agecon.purdue.edu/), Purdue University. The intertemporal extensions (GTAP-INT, GTAP-RE) were developed by Pham Van Ha and Tom Kompas at the University of Melbourne. ORANI-G is developed and maintained by the [Centre of Policy Studies](https://www.copsmodels.com/), Victoria University (formerly Monash University). TEEMS-compatible syntactic modifications were made by Matthew Cantele.
