# How the score is counted

The score compares Migna US Quality with the S&P 500. Field names in the record files are given in `code`.

## The portfolio

- **Added.** A company is added when Migna publishes it (`found`). It joins the portfolio at the opening price of the first US
  session after that (`entry_day`, `entry_price`). Its rules are fixed before it is added.
- **Weights.** The portfolio holds every company in it in equal parts and is rebalanced to equal parts at every close.
- **Each day.** The portfolio moves by the simple average of its companies' moves that day, each from the previous close. A
  company joining that day moves from its entry open.
- **Removed.** A company leaves at a close, for one of these reasons:
  - **Its price reached our estimate:** the first close at or above the estimate it was added on (`estimate_at_find`). This is a
    close, not an intraday high, and never a later estimate.
  - **Its time ran out:** one year after it was added (90 days for companies added before 18 October 2026), at the close of
    `judging_clock_end`.
  - **Our estimate came down to the price:** that night's estimate fell to or below the close, by our valuation method, its results
    or our data. The reason says which.
  - **It no longer passes the quality test:** at the close of the first failing night when its results caused it. Otherwise only
    once it has failed on five nights in a row, at the fifth close.
  - **The standard changed:** a raised threshold applies to every company in the portfolio on the same night.
  - **A corporate event:** a takeover ends at the price paid, on completion. A delisting ends at the last traded price. A
    suspension holds the last close until trading resumes. A spin-off is followed as the package a holder received.
  - **Withdrawn, our error:** we published it in error. It is valued at the close of the last day it was listed, and its reason
    is published as a correction.
  The removal date is never earlier than the day the removal could be seen. A removed company stays in every figure, gains and
  losses alike. A company that qualifies again is added again as a new entry, never resumed.
- **Then.** From the next session the portfolio is split equally across the companies still in it.
- **None in it.** The portfolio holds cash, earning nothing.
- **Nothing else.** There are no caps, no cash buffer, no trimming and no timing, and no trading costs are taken off.
- **Dividends.** Included. Prices are dividend-adjusted, so a dividend is reinvested on its ex-date (`basis` in each file). The
  `*_raw` fields are the prices as traded.

## The benchmark

The S&P 500 is SPY's total return over the same closes, with its dividends reinvested on the ex-date.

## The public start

The public score counts from **16 October 2026**, the first session after the first night sealed on Bitcoin (the proof for the
15 October close, written before 16 October's open). The portfolio and SPY are both set to 100 at the 15 October close.
`BASE_2026-10-15.json` holds the companies in the portfolio at that close, with their prices and SPY's level. The score at any
later close is the portfolio's change from that base minus SPY's change from that base, in percentage points.

Each record file's `pot_pct` is the portfolio's change from its first entry (18 September 2026). To read it from the public start,
compound: (1 + pot_pct at the close / 100) / (1 + pot_pct at 15 October / 100) - 1. For SPY, divide its total-return level at the
close by its total-return level in the base file.

## Corrections

A sealed file is never rewritten. A correction is a new, separately named file, `CORRECTION_<close>.json`, saying what changed,
when and why, and the sealed file stands beside it.
