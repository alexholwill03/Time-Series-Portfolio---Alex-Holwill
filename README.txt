Time Series Analysis Portfolio
Alex Holwill
Honours Time Series Analysis, University of Cape Town, 2026

Rendered site: https://alexholwill03.github.io/Time-Series-Portfolio---Alex-Holwill/

WHAT THIS IS

A portfolio of four time series projects, worked tutorial answers, a reflective commentary, a journal and an AI use log, written R.

  Project 1 - Forecast comparison for the SA 10-year bond yield (ARIMA against benchmarks)
  Project 2 - Volatility of monthly yield changes (GARCH and GJR-GARCH)
  Project 3 - Harmonic regression for Nottingham Castle temperatures (nottem)
  Project 4 - Hidden Markov model for regimes in yield changes

FILES

  index.qmd - Main Quarto source; renders the whole site
  _journal.md - Weekly journal, included in index.qmd
  _ai-use-log.md - AI use log, included in index.qmd
  _quarto.yml - Quarto website settings
  data/IRLTLT01ZAM156N.csv - Raw bond yield data from FRED (downloaded 4 September 2026)
  data/za_yield_clean.rds - Cleaned series (March 1975 onwards), written when index.qmd renders
  _freeze/ - Stored results from the last render (Quarto freeze)
  Time-Series-Portfolio---Alex-Holwill.Rproj - RStudio project file

The rendered site is published from the gh-pages branch.

HOW TO REPRODUCE

1. Install R (4.6.1 was used), RStudio and Quarto.
2. Install the R packages:
     tidyverse, timetk, tsibble, feasts, fabletools, fable, tibbletime,
     lubridate, tseries, knitr, forecast, rugarch, FinTS, depmixS4, dlm,
     fpp2, SimDesign
3. Open Time-Series-Portfolio---Alex-Holwill.Rproj and render index.qmd (or run "quarto render" in the project folder).

Because freeze is set to auto, Quarto reuses the stored results in _freeze/ unless index.qmd changes. Delete _freeze/ to force every chunk to run again. Random seeds are set wherever results depend on simulation or random starting values. The exact package versions are listed in the Software section of the appendix (sessionInfo()).

The Project 3 data and the tutorial datasets come from R packages or are entered in the code, so data/IRLTLT01ZAM156N.csv is the only external file needed.
