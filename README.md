# Record fingerprints

A daily fingerprint of an investment research app's public record: every company the app covers with its reading that day, the
open finds, and every find made so far with its move.

Each file in `proofs/` holds one line:

    <close>  sha256 <hash>  companies <n>  open <n>  found <n>  judged <n>

where `<close>` is the market close the record is read at and `<hash>` is the SHA-256 of that record file. Beside it,
`<close>.txt.ots` is an [OpenTimestamps](https://opentimestamps.org) proof that the line existed by then, anchored in the Bitcoin
blockchain, which nobody here can change or back-date. `registration_<day>.txt` lines register the app's model portfolios by
date and fingerprint only.

To check a night: `pip install opentimestamps-client`, then `ots verify proofs/<close>.txt.ots` (it reports the Bitcoin block that
holds it). When a record file is published, its SHA-256 (`sha256sum <close>.json`) must equal the hash in `proofs/<close>.txt`.

Corrections are listed in `CORRECTIONS.md`, each with what changed, when and why; earlier versions are kept in `corrections/`,
never deleted.

Note: the lines for the closes of 20 October to 20 November 2026 read `open 0`. That was a counting fault in the proof line
only, since fixed; the stamped record files themselves carry the right number of open finds.
