# Corrections

Each correction says what changed, when and why. An earlier version is kept in `corrections/`, never deleted.

## 2026-10-16.later-1700 -- corrected 24 November 2026

On 18 October 2026 at 13:00 UTC the fingerprint job re-read the 16 October close and stamped this line, which
`proofs/2026-10-16.later-1700.txt.ots` proves:

    2026-10-16  sha256 8967cb46f3b659822b3ab0b5003c94619dd44b2d18dbde3deee10fcbeb24939f  companies 665  open 6  found 17  judged 0

On 19 October at 13:00 UTC a second re-read wrote its own line over the same file, because the job named a re-read by its time of
day only, and then could not stamp it, because the proof already existed. From then until 24 November the file held the 19
October line, which does not match the proof. The stamped 18 October line is restored. The 19 October line was never stamped;
it is kept as `corrections/2026-10-16.later-1700.19-october.unstamped.txt`. The job now never reuses a name that already has a
proof.

## 2026-11-20 -- noted 24 November 2026

The record for the 20 November close was first written at 03:07 UTC on 21 November with one company, PepsiCo, counted twice (a
fault since fixed). It was replaced at 03:57 UTC, before the record was sealed. The stamped file is the 03:57 one (sha256
567427923bc07b2799e65c8a59bdad516ffb32c1f2041449ddadc8bccb37ce88); the 03:07 file (sha256
a17f238d3be40c24598a688cc3cd6d2875a1c9c9cff08a7d62841b29c281d87a) is in no proof and is kept with the record files.

## SCORE_DAILY.json -- withdrawn 25 November 2026

A first `SCORE_DAILY.json`, published on the morning of 25 November, counted the score from the close of 15 October. The public
score counts from the close of 20 October (`METHOD.md`), so that file contradicted the method and was withdrawn the same morning.
The series is published again only when it starts at the 20 October close. The withdrawn file stays in this repository's history.

Each entry says what changed, when and why. The sealed files stand as written beside them. Dates are closes; times are UTC.

**Grindr, withdrawn, our error (3 November).** Its June-quarter filing, public by 2 October, showed debt that our read of 2 October
took as none; with it, the company did not meet our bar that day. It is valued at the 3 November close, the last day it was listed,
and stays in every figure. Files from 3 November show it judged on that day.

**Valmont, a withdrawal reversed (18 November).** Valmont was withdrawn on 2 November under a rule we had already dropped on 29
October. On 18 November the withdrawal was reversed: Valmont counts from its 2 November entry, as if it had never been withdrawn.
The sealed files of 2 to 17 November do not carry it, because they were written while it stood withdrawn. Its holding on each of
those days, with its move and close, is in `SCORE_DAILY.json`.

**PepsiCo, reinstated (19 November).** PepsiCo was removed on 30 October because of our own logged error. On 19 November it was
reinstated as if the error had not happened: it continues as the company added on 23 September, entry at the 24 September open.
Its re-entry of 18 November is withdrawn as our error. The sealed files of 3 to 17 November do not carry it as held.

**The portfolio figure in the sealed files of 6 to 17 November.** These files' `pot_pct` was computed without Valmont and PepsiCo,
which were then withdrawn or removed. After their reversal and reinstatement (above), the portfolio for those closes is the one in
`SCORE_DAILY.json`. The 10 November file also repeats 9 November's figure (14.117), because that night's run failed; the 10 November
figure is in `SCORE_DAILY.json`.

**20 November, a first write replaced.** The 20 November file was first written at 03:07 on 21 November and counted PepsiCo twice.
It was replaced at 03:57, before it was sealed; the sealed and stamped file is the 03:57 one.

**Check Point, withdrawn, our error (24 November).** Its September-quarter results, public on 2 November, showed revenue down 1% and
underlying earnings up 1%, and the company said its recovery was taking longer than expected. Our final review of 6 November read only
its annual report; with the quarter's results it would have held it back. It counted from the 9 November open to the 24 November close.

**Liquidity Services, withdrawn, our error (24 November).** Its full-year results of 19 November guided next quarter's earnings to
about flat and said a slowdown in one segment would last the next few quarters; our final review read that as no guidance. It counted
from the 23 November open to the 24 November close. The 23 November file showed it as having reached our estimate, because the record
read the wrong estimate (32.94 instead of the 36.48 it was added on); corrected. The 24 November file repeats that error (judged on
23 November, +0.98%, portfolio 11.061%); with the withdrawal it is +2.6% and the portfolio 11.099%.
