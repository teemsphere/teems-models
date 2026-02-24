# teems-models

Model files for the [Trade and Environment Equilibrium Modeling System (TEEMS)](https://teemsphere.github.io/). Each directory contains a TABLO model specification (`.tab`) and a standard closure file (`.cls`) vetted for use with the [`teems`](https://github.com/teemsphere/teems) R package.

## Models

### GTAPv6 — GTAP Version 6.2

| | |
|---|---|
| **Type** | Static |
| **Date** | September 2003 (TEEMS modifications February 2026) |
| **Files** | `GTAPv6.tab`, `GTAPv6.cls` |

The [classic GTAP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=2458), version 6.2. Includes multiple margin sectors, the CDE regional household demand system, welfare decomposition, import-augmenting technical change, and Baldwin-type capital accumulation effects.

**References:**
- Hertel, T.W. and M.E. Tsigas, "Structure of the Standard GTAP Model", Chapter 2 in T.W. Hertel (ed.) *Global Trade Analysis: Modeling and Applications*, Cambridge University Press, 1997.
- McDougall, R.A., "A New Regional Household Demand System for GTAP", GTAP Technical Paper #20, Center for Global Trade Analysis, Purdue University.
- Hertel, T.W., K. Itakura and R.A. McDougall, "GTAP.TAB: The Standard GTAP Model", GTAP Technical Paper, Center for Global Trade Analysis, Purdue University.

### GTAPv7 — GTAP Version 7.0

| | |
|---|---|
| **Type** | Static |
| **Date** | June 2017 (TEEMS modifications February 2026) |
| **Files** | `GTAPv7.tab`, `GTAPv7.cls` |

The [standard GTAP model](https://www.gtap.agecon.purdue.edu/resources/res_display.asp?RecordID=6438), version 7.0. Supersedes version 6.2 with activity-specific factor income taxes, endowment type flags, refined welfare decomposition distinguishing output and income tax effects, aggregate demand quantity indices, and world GDP indices.

**References:**
- Corong, E.L., T.W. Hertel, R.A. McDougall, M.E. Tsigas, and D. van der Mensbrugghe. "The Standard GTAP Model, Version 7." *Journal of Global Economic Analysis*, 2(1), 1-119, 2017. https://doi.org/10.21642/JGEA.020101AF

### GTAP-INT — GTAP-INT Version 1

| | |
|---|---|
| **Type** | Intertemporal (based on GTAPv6.2) |
| **Date** | January 2015 |
| **Files** | `GTAP_INT.tab`, `GTAP_INT.cls` |

An intertemporal extension of the GTAPv6.2 model developed by Kompas and Van Ha. Adds a time dimension for dynamic analysis with forward-looking investment and capital accumulation.

**References:**
- Van Ha, P. and T. Kompas, "Solving intertemporal CGE models in parallel using a singly bordered block diagonal ordering technique." *Economic Modelling*, 52, 3-12, 2016. https://doi.org/10.1016/j.econmod.2015.07.011
- Kompas, T. and P. Van Ha, "The 'curse of dimensionality' resolved: The effects of climate change and trade barriers in large dimensional modelling." *Economic Modelling*, 80, 103-110, 2019. https://doi.org/10.1016/j.econmod.2018.08.011

### GTAP-RE — GTAP-RE Version 1

| | |
|---|---|
| **Type** | Intertemporal with rational expectations (based on GTAPv7.0) |
| **Date** | May 2025 |
| **Files** | `GTAP_RE.tab`, `GTAP_RE.cls` |

An intertemporal rational expectations extension of the GTAPv7.0 model. Incorporates forward-looking agent behavior and rational expectations dynamics for multi-period trade and environmental policy analysis.

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

The GTAP modeling framework is developed and maintained by the [Center for Global Trade Analysis](https://www.gtap.agecon.purdue.edu/), Purdue University. The intertemporal extensions (GTAP-INT, GTAP-RE) were developed by Pham Van Ha and Tom Kompas at the University of Melbourne. TEEMS-compatible syntactic modifications were made by Matthew Cantele.
