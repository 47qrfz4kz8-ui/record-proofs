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

The public score counts from the **20 October 2026 close**, the first record file published with its companies and prices, so
every figure can be checked from public sealed files alone (Harry, 25 November 2026). The portfolio and SPY are both set to 100 at
the 20 October close; the first session counted is 21 October. The score at any later close is the portfolio's change from that
base minus SPY's change from that base, in percentage points.

Each record file's `pot_pct` is the portfolio's change from its first entry (18 September 2026). To read it from the public start,
compound: (1 + pot_pct at the close / 100) / (1 + pot_pct at 20 October / 100) - 1. For SPY, divide its total-return level at the
close by its level at 20 October. Those levels are in `SCORE_DAILY.json`; the record files' `spy_close` and `spy_entry` are
SPY's price levels, without its dividends.

**The research record.** Migna's record from its first entry, 18 September 2026, is kept and stays in the files. It is the
research record: it is never presented as the public track record.

## Where the files depart from these rules, dated

The record files are sealed as written, so a rule adopted later does not change an earlier file. Each departure a reader will meet:

- **Our estimate on the day it was added (from the 23 October file).** Earlier files carried a later revision of our estimate for
  some companies. From the 23 October file each company carries the estimate as it stood on the day it was added: Paychex moves
  from 137.28 to 126.79 and Jack Henry from 192.85 to 202.21. A company's removal on reaching our estimate is judged only against
  that figure.
- **Joining when readers could first see it.** A company joins at the first open after it reached readers, which can be later
  than the session after its `found` date: T-Mobile US and TransUnion (recorded 20 October, shown to readers 22 October), Rollins
  and TJX (sealed before they reached readers), Cognex (held back a night by our own system). The `published` field, which shows
  when a company reached readers, is filled for some companies in the files of 20 October to 6 November and empty after; the entry
  day in each file is the authority. `CORRECTION_2026-11-06.json` lists four entry prices as traded (Rollins, T-Mobile US,
  TransUnion, TJX) that differ from the 6 November file, because their entry days were restated to the first open readers could
  have had.
- **A ruling takes effect at the first close after it (from 18 November).** Where a ruling ended a company and the code caught up
  later, the ending is dated to the first close after the ruling, by a correction, and the sealed files from the days between
  still show it held. Lennox is the case.
- **An ending caused by our own error is undone (from 19 November).** When a company was removed because of our own logged error,
  it is reinstated as if the error had not happened, by a dated correction. This is the one exception to "never resumed".
  PepsiCo is the case: it continues as the company added on 23 September (entry at the 24 September open), and its 18 November
  re-entry is withdrawn as our error.
- **A withdrawal reversed (18 November).** Valmont was withdrawn on 2 November under a rule we had already dropped. The withdrawal
  was reversed by a dated correction, so Valmont counts from its 2 November entry; the 18 November file is the first to show it.
- **Our estimate's rounding (from the 24 November file).** Estimates are written to two decimals from the 24 November file
  (PepsiCo 178.5734 becomes 178.57, Cadence 336.8585 becomes 336.85). No company's removal turns on the difference.
- **The portfolio figure in the files (from 6 November).** `pot_pct` is in every file from 6 November. Earlier files carry each
  company's rows, from which it can be rebuilt, and `performance_pct`, the average company's move, which is a different figure. The files of 6 to 17
  November computed it before Valmont's and PepsiCo's restorations (CORRECTIONS.md); `SCORE_DAILY.json` carries the figure as it
  stands, with each day's holdings.

## The daily score

`SCORE_DAILY.json` lists the score at every close from the base: the portfolio and SPY as levels (100 at the 20 October close),
the gap in points, and the companies held that day, each with its move and close. The portfolio's move each day is the simple
average of those moves, so every line can be checked without rebuilding the rules.

## Corrections

A sealed file is never rewritten. A correction is a new, separately named file, `CORRECTION_<close>.json`, saying what changed,
when and why, and the sealed file stands beside it.
