## Date: Week of 6 September

### Topic: Finding data & EDA on the bond yields

#### What I did & what I learned:

- Wanted to do my portfolio on interest rates, so I found the South African 10-year government bond yield on FRED (monthly, 1957 to 2026): https://fred.stlouisfed.org/series/IRLTLT01ZAM156N
- Set up the data and did the EDA: time plot, summary stats, rolling sd, ACF/PACF and unit root tests
- Something is off before the mid-1970s. Most months show no change at all and the yield only takes about 20 different values, so it doesn't look like a market rate. Cut the sample at January 1976 for now
- ADF and KPSS both say the yield has a unit root, so I'll be working with changes

#### Difficulties and open questions:

- Setting up the GitHub Pages site with Quarto took way longer than expected
- Why does the data behave so differently before 1976? Is it a different definition, or did something actually change?

#### What to do next:

- Do tut 1
- Keep looking into the pre-1976 data

## Date: Week of 13 September

### Topic: Tutorial 1

#### What I did & what I learned:

- Did tut 1: the steps in the forecasting process, features to expect in different series, and reading time plots, ACFs and PACFs
- The Q6 series looked almost exactly like my bond yield: an ACF that barely decays and one big PACF spike at lag 1. Nice to see the textbook unit root pattern in my own data

#### Difficulties and open questions:

- Q1 (the biscuit manufacturer) is very open-ended, so it was hard to know how much detail to give

#### What to do next:

- Start projects 1 and 2 on the bond yield

## Date: Week of 20 September

### Topic: Projects 1 and 2

#### What I did & what I learned:

- Project 1: compared ARIMA(0,1,1) with naive, drift and seasonal naive using rolling-origin cross-validation
- ARIMA only beats naive one month ahead, and only by about 3%. After that the yield is basically a random walk
- Fun one: seasonal naive and naive give exactly the same RMSE at 12 months, because 12 months ahead both forecasts are just the last value
- Project 2: fitted GARCH and GJR-GARCH with normal and t errors. GARCH(1,1) with t errors wins, with a half-life of about 7.5 months and no sign of asymmetry

#### Difficulties and open questions:

- forecast and fabletools both have an accuracy() function and kept masking each other. Had to load forecast later and call it with forecast::
- The cross-validation with 365 origins is slow to render
- Took a while to work out what rugarch calls everything (omega, alpha1, beta1, shape)

#### What to do next:

- Do tut 2 on exponential smoothing

## Date: Week of 27 September

### Topic: Tutorial 2

#### What I did & what I learned:

- Wrote my own SES function, estimated it with optim, and compared it with ses(). Also did Holt's method and simulated from both models to see if I could get the parameters back
- My estimates match ses() to about 3 decimal places, which was satisfying
- In the books data, Holt's alpha and beta come out almost zero, so it's basically fitting a straight line

#### Difficulties and open questions:

- My prediction intervals didn't match ses() at first. ses() divides the SSE by T minus the number of parameters, not by T
- The initial level and trend are hard to recover in the simulations, because they only affect the first few observations

#### What to do next:

- Do tut 3 on dynamic linear models

## Date: Week of 4 October

### Topic: Tutorial 3

#### What I did & what I learned:

- Fitted the random walk plus noise model to the Nile data, then dealt with missing years, the basic structural model for co2, and seasonality with trig terms
- With 20 missing years, the filtered standard error just keeps growing, while the smoothed one peaks in the middle of the gap. Makes sense once you see it
- q = 2 harmonics beat the 12 seasonal dummies on AIC

#### Difficulties and open questions:

- The diffuse prior makes the first year of the co2 filter jump all over the place
- The q = 1 trig model didn't converge properly (code 52)

#### What to do next:

- Start project 3: harmonic regression on the bond yield

## Date: Week of 11 October

### Topic: Project 3 (and switching datasets)

#### What I did & what I learned:

- Started harmonic regression on the bond yield, but the periodogram and ACF showed no yearly cycle at all, so the Fourier terms had nothing to fit
- Switched to the nottem dataset (Nottingham Castle temperatures), did its EDA, and then fitted harmonic regression with ARMA errors against a SARIMA baseline
- The 12-month cycle holds about 84% of the periodogram power. Harmonic regression was slightly more accurate than SARIMA on the 24 test months

#### Difficulties and open questions:

- Lost a few days on the bond yield before accepting it wasn't the right data for this method
- AICc can't compare the harmonic regression with the SARIMA, because the SARIMA uses a seasonal difference
- K = 2, 3 and 4 harmonics are almost tied on AICc, so the choice isn't clear

#### What to do next:

- Do the HMM tut and project 4

## Date: Week of 18 October

### Topic: HMM tutorial and Project 4

#### What I did & what I learned:

- Tut 4: simulated an HMM, coded Viterbi on the log scale, worked through likelihoods by hand and with matrices, and fitted a two-state Poisson HMM to the earthquake data
- My earthquake fit matched depmixS4 almost exactly, and the Viterbi paths were identical
- Project 4: wrote a Gaussian HMM for the yield changes from scratch (scaled forward algorithm, decoding, forecasts) and compared it with an iid normal model

#### Difficulties and open questions:

- Had to scale the forward algorithm, otherwise the likelihood underflows over almost 600 months
- The fits depend on starting values, so I had to use lots of random starts

#### What to do next:

- Go back through all the projects and tuts and check everything

## Date: Week of 25 October

### Topic: Checking my work

#### What I did & what I learned:

- Finally found why the early data is weird: the Reserve Bank set a fixed pattern of rates on government stock until February 1975. Moved the start of the sample to March 1975 and reran everything
- Found that my 3-state HMM had collapsed: one state had a standard deviation of 0 sitting on the months with no change. Added a floor of 0.05 on the state standard deviations. After that BIC picked 2 states, and my fit matched depmixS4
- Went through and wrote up the interpretations for the EDA, all four projects and the tuts

#### Difficulties and open questions:

- Changing the start date meant rechecking every result that depended on it
- The HMM still doesn't forecast better than the iid normal model on the test months, probably because recent volatility sits between the two states

#### What to do next:

- Write the reflective commentary and AI use log, then submit
