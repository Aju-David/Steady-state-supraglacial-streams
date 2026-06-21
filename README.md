# Steady-state-supraglacial-streams

This repository contains a Python-based analysis workflow for studying the properties of supraglacial meltwater streams across five glaciers: Siachen and Rongbuk (High Mountain Asia), Fountain (Canadian Arctic), and Vonbreen and Veteranbreen (Svalbard, Norway).  The workflow is organized into three sequential interactive python notebooks covering data loading, analysis, and figure generation. All results, fitted parameters, goodness-of-fit statistics, and figures are generated automatically by running the notebooks in order.

## Description of notebooks

### `01_Loading.ipynb` — Data Loading & Configuration
Loading notebook; It defines all parameters including the alpha values that determine the slope trend (constant, upward, downward) and the stream metadata registry containing group names, labels, colors, markers, and trend types for all 10 glacier streams across 5 glaciers (Siachen, Rongbuk, Fountain, Vonbreen, and Veteranbreen). All CSV files are loaded from the `Stream_csv/` folder, and for each stream the downstream distance (`dist_N`) and segment ID (`segment_id`) are computed. Rows with missing elevation values are removed. The loaded and configured data is saved to `data.pkl` for use in subsequent notebooks.

### `02_Analysis.ipynb` — Stream data Analysis

This notebook performs all quantitative analysis on the loaded glacier stream data. It sequentially computes:

* Sinuosity — arc length and chord length per segment, cumulative sinuous and normal lengths
* Segment means — mean velocity, elevation, relief, length and maximum elevation per segment using all the points.
* Slope — `slope_l` (along sinuous path, computed as elevation difference between neighbouring segments divided by their length difference) and `slope_d` (along flowline path, computed as delta-z over normal length per segment) Refere supplementary Text S1 for more details.
* Flux of sinuosity — sinuosity × velocity per segment.
* beta'1 (slope profile parameter) — fitted from the slope profile equation `S = β'₁ · x^((α−1)/2)` using OLS through the origin, with corresponding standard error.
* beta'2 (elevation profile parameter) — fitted from the elevation integral equation using OLS, with corresponding standard error.
* Goodness of fit metrics — R², Adjusted R², RMSE, MAE, NMRSE and Pearson r for both the slope profile fit and the elevation profile fit.
Results are saved to `analysis.pkl` for use in the plotting notebook.

### `03_Plotting.ipynb` — Figures & Export csv

This notebook generates all manuscript figures and exports the fitted parameter values. It produces:

* Fig 2 ab — Normalized slope and elevation profiles for constant-trend streams (Siachen 1–3, Veteranbreen)
* Fig 3 ab — Normalized slope and elevation profiles for upward-trend streams (Fountain 1–2, Vonbreen 1–2)
* Fig 3 cd — Normalized slope and elevation profiles for downward-trend streams (Siachen 4, Rongbuk)
* Fig 4 ab — Sinuosity spatial pattern and observed vs predicted sinuosity scatter plot for all streams
* Fig S5 — Elevation profiles along flowline distance for each glacier group
* Fig S7 — Flux profiles along flowline distance for each glacier group
* Fig S8 — Sinuosity variation and slope KDE distributions for each trend regime (constant, upward, downward) in separate panels
* A CSV file (`beta'_values.csv`) containing the fitted `β'₁ ± SE` and `β'₂ ± SE` values for all 10 streams formatted to 3 significant figures.

## Description of Folders
### `Stream_csv/` — Input Data
Contains the raw CSV files for all 16 streams across the 5 glacier systems. Each file contains point-level (5m-Interval measurements of position (`x`, `y`), along-stream distance (`distance`), surface elevation (`elev`), surface velocity (`velocity`), and `relief`. Files are named by stream codes (`sia_1.csv` through `vet_1.csv`).
### `Output/` 
Stores all the plots and csv file.
### `Stream_kml`
Containes all the kml files of the 16 deliniated stream centerlines. Files are named by stream codes
