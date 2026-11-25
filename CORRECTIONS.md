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
