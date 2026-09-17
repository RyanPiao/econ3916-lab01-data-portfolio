## Deflating Economic Data — Nominal vs. Real

### Objective
Convert nominal U.S. wage and consumer price series into constant-dollar terms to separate real changes in purchasing power from changes driven by inflation.

### Methodology
- **Data acquisition:** Retrieved the Consumer Price Index (CPI) and average hourly earnings directly from FRED's public CSV endpoint, with no API key, using a reusable `load_fred()` loader that returns date-indexed series.
- **Deflation function:** Implemented `deflate_series(nominal, cpi, base_year)`, which rescales each observation by the ratio of the base-year price level to the contemporaneous price level: real_t = nominal_t × CPI_base / CPI_t.
- **Wage deflation:** Converted monthly average hourly earnings to constant 2020 dollars and compared the nominal and real paths over the full sample.
- **Frequency alignment:** Matched irregularly dated Big Mac price observations to monthly CPI with an as-of merge, so each price is paired with the most recent available price level rather than dropped for lacking an exact date match.
- **Big Mac deflation:** Deflated the U.S. Big Mac price to 2020 dollars and decomposed its nominal change into general inflation (CPI) and a relative price change.
- **Interactive explorer:** Built an `ipywidgets` + `matplotlib` dashboard in Google Colab with a series selector, a nominal/real toggle, and a base-year slider (2000–2025). It reports first-to-last percentage changes in both nominal and real terms.

### Key Findings
- **Wages:** Nominal average hourly earnings rose from $[YOUR VALUE] to $[YOUR VALUE], while real earnings in 2020 dollars moved from $[YOUR VALUE] to $[YOUR VALUE]. Much of the nominal gain reflects inflation rather than higher purchasing power.
- **Big Mac:** The nominal price rose [YOUR VALUE]% while CPI rose [YOUR VALUE]% over the same dates, leaving a real increase of [YOUR VALUE]%. The Big Mac became more expensive *relative to the overall consumer basket*, which shows that "real" means relative to the average price level, not zero growth.
- **Base-year invariance:** The explorer shows that changing the base year shifts the level of a real series but leaves its growth rate unchanged, because the base-year CPI is a constant that cancels in any ratio. Conclusions about real growth therefore do not depend on the choice of base year.
- **Interpretive caveats:** Measured real wage growth is sensitive to the choice of deflator (CPI vs. PCE), the sample endpoints, and the earnings concept (cash wages exclude benefits). Composition effects also matter; the 2020 spike in average earnings reflected job losses concentrated among lower-wage workers, not broad pay gains.
